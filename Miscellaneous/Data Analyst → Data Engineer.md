# Data Analyst → Data Engineer: Action Plan

> An action plan built around your existing tools and your actual starting point.
> Several Phase 1 items are already complete — you’re ahead of most analyst-track candidates.

-----

## ✅ Already Done — Your Existing Engineering Foundations

You’ve already implemented practices that many working DEs don’t have. These are not small things:

- **Modular Python packages** with separate config files and environment variables
- **Error handling and logging** baked into your scripts
- **SnowflakeConnector class** — reusable, encapsulated database access
- **Excel export** on query completion — a working output layer
- **Modified Gitflow** — main/dev branches, UAT hook on push, manual prod promotion

This means you’re not learning to code like an engineer. You’re already doing it. The gap is about **pipeline architecture, orchestration, and DE-native tooling** — not fundamentals.

-----

## Phase 1 — Extend What You Have

**Weeks 1–3 · Close the remaining analyst-to-engineer gaps**

Your package is solid. These steps harden the edges that typically separate analyst scripts from true pipeline components.

-----

### 1. Redirect Excel outputs to S3 as CSV or Parquet alongside or instead of Excel

`Python` `S3` `boto3`

Your package already exports query results to Excel. Add boto3 and write those same results to an S3 `processed/` prefix as CSV or Parquet. Excel stays for stakeholders; S3 becomes the data layer handoff.

```python
import boto3
import pandas as pd
from io import BytesIO
from datetime import datetime

def export_to_s3(df: pd.DataFrame, bucket: str, source_name: str, fmt: str = "parquet") -> str:
    """Export a DataFrame to S3 as parquet or csv. Returns the S3 key."""
    s3 = boto3.client("s3")
    date_prefix = datetime.utcnow().strftime("%Y/%m/%d")
    key = f"processed/{source_name}/{date_prefix}/{source_name}.{fmt}"

    buffer = BytesIO()
    if fmt == "parquet":
        df.to_parquet(buffer, index=False)
    else:
        df.to_csv(buffer, index=False)
    buffer.seek(0)

    s3.put_object(Bucket=bucket, Key=key, Body=buffer.getvalue())
    return key
```

-----

### 2. Add a retry/backoff mechanism to your SnowflakeConnector

`Python` `SQLAlchemy` `Snowflake`

You have the class — now harden it. Use `tenacity` to handle transient connection failures gracefully. Production pipelines assume network flakiness.

```python
from tenacity import retry, stop_after_attempt, wait_exponential, retry_if_exception_type
from sqlalchemy.exc import OperationalError
import logging

logger = logging.getLogger(__name__)

class SnowflakeConnector:
    # ... your existing __init__ and setup ...

    @retry(
        retry=retry_if_exception_type(OperationalError),
        wait=wait_exponential(multiplier=1, min=2, max=30),
        stop=stop_after_attempt(4),
        reraise=True
    )
    def execute_query(self, sql: str) -> pd.DataFrame:
        """Execute a query with automatic retry on transient failures."""
        logger.info("Executing query", extra={"sql_preview": sql[:120]})
        with self.engine.connect() as conn:
            return pd.read_sql(sql, conn)
```

-----

### 3. Standardize logging to structured JSON format

`Python`

If your logs are human-readable strings today, switch to structured JSON. JSON logs are parseable by CloudWatch, Datadog, and any log aggregator — expected in cloud pipeline environments.

```python
import logging
import json

class JsonFormatter(logging.Formatter):
    def format(self, record: logging.LogRecord) -> str:
        log_record = {
            "timestamp": self.formatTime(record),
            "level": record.levelname,
            "logger": record.name,
            "message": record.getMessage(),
        }
        # Merge any extra fields passed via extra={}
        for key, val in record.__dict__.items():
            if key not in logging.LogRecord.__dict__ and key not in log_record:
                log_record[key] = val
        return json.dumps(log_record)

def get_logger(name: str) -> logging.Logger:
    handler = logging.StreamHandler()
    handler.setFormatter(JsonFormatter())
    logger = logging.getLogger(name)
    logger.setLevel(logging.INFO)
    logger.addHandler(handler)
    return logger

# Usage
logger = get_logger(__name__)
logger.info("Query complete", extra={"rows": 1200, "source": "billing_db"})
# Output: {"timestamp": "...", "level": "INFO", "message": "Query complete", "rows": 1200, "source": "billing_db"}
```

-----

### 4. Add a run manifest to each pipeline execution

`Python` `S3` `Snowflake`

At the end of each run, write a small JSON metadata record: timestamp, rows processed, source, destination, status, errors. This is the foundation of pipeline observability.

```python
import json
import boto3
from datetime import datetime, timezone
from typing import Optional

def write_run_manifest(
    bucket: str,
    pipeline_name: str,
    rows_processed: int,
    source: str,
    destination: str,
    status: str,                     # "success" | "failure"
    error: Optional[str] = None
) -> None:
    manifest = {
        "pipeline": pipeline_name,
        "run_timestamp": datetime.now(timezone.utc).isoformat(),
        "status": status,
        "rows_processed": rows_processed,
        "source": source,
        "destination": destination,
        "error": error,
    }
    key = f"manifests/{pipeline_name}/{manifest['run_timestamp']}.json"
    boto3.client("s3").put_object(
        Bucket=bucket,
        Key=key,
        Body=json.dumps(manifest, indent=2)
    )

# Usage at end of pipeline
write_run_manifest(
    bucket="my-data-bucket",
    pipeline_name="billing_extract",
    rows_processed=len(df),
    source="snowflake.billing_db",
    destination="s3://my-data-bucket/processed/billing/",
    status="success"
)
```

**Goal:** Your existing package becomes a first-class pipeline component — hardened, observable, and cloud-output-ready.

-----

## Phase 2 — Build an End-to-End Pipeline with Your Current Tools

**Weeks 4–10 · Architect like an engineer**

You already have the components. Now wire them together intentionally into a layered architecture.

-----

### 1. Design and implement a formal S3 layer structure

`S3` `Python` `boto3`

Structure S3 with `raw/`, `staging/`, and `processed/` prefixes with consistent date partitioning. This turns ad-hoc S3 usage into a real data lake pattern.

```
s3://my-data-bucket/
├── raw/
│   └── source_name/
│       └── YYYY/MM/DD/
│           └── source_name_HHMMSS.json
├── staging/
│   └── source_name/
│       └── YYYY/MM/DD/
│           └── source_name_cleaned.parquet
└── processed/
    └── source_name/
        └── YYYY/MM/DD/
            └── source_name_final.parquet
```

```python
from datetime import datetime

def build_s3_key(layer: str, source: str, extension: str) -> str:
    """Generate a consistent, partitioned S3 key."""
    now = datetime.utcnow()
    return (
        f"{layer}/{source}/"
        f"{now:%Y}/{now:%m}/{now:%d}/"
        f"{source}_{now:%H%M%S}.{extension}"
    )

# Examples
build_s3_key("raw", "billing_portal", "json")
# → "raw/billing_portal/2025/03/15/billing_portal_143022.json"

build_s3_key("processed", "billing_portal", "parquet")
# → "processed/billing_portal/2025/03/15/billing_portal_143022.parquet"
```

-----

### 2. Replace an Alteryx workflow with a Python + SQL script

`Alteryx` `Python` `SQL` `Redshift`

Pick one Alteryx workflow and rebuild it using your existing package. Below is the pattern to follow — your SnowflakeConnector replaces Alteryx’s input tool, pandas replaces the transform tools, and SQLAlchemy replaces the output tool.

```python
import pandas as pd
from your_package.connectors import SnowflakeConnector, RedshiftConnector
from your_package.logger import get_logger

logger = get_logger(__name__)

def run_billing_transform():
    sf = SnowflakeConnector()
    rs = RedshiftConnector()

    # 1. Extract (replaces Alteryx Input tool)
    raw = sf.execute_query("SELECT * FROM billing_db.raw.invoices WHERE invoice_date >= CURRENT_DATE - 30")
    logger.info("Extracted from Snowflake", extra={"rows": len(raw)})

    # 2. Transform (replaces Alteryx formula/join/filter tools)
    df = (
        raw
        .rename(columns={"inv_dt": "invoice_date", "cust_id": "customer_id"})
        .dropna(subset=["customer_id"])
        .assign(invoice_amount_usd=lambda x: x["invoice_amount"] / 100)
        .query("invoice_amount_usd > 0")
    )

    # 3. Load (replaces Alteryx Output tool)
    rs.load_dataframe(df, schema="staging", table="invoices_30d", if_exists="replace")
    logger.info("Loaded to Redshift", extra={"rows": len(df), "table": "staging.invoices_30d"})

if __name__ == "__main__":
    run_billing_transform()
```

-----

### 3. Structure your Snowflake SQL into explicit transformation layers

`SQL` `Snowflake`

Organize SQL files into three tiers in your project. This is the exact folder structure dbt uses — you’re building the mental model now.

```
sql/
├── staging/
│   └── stg_invoices.sql       ← rename, cast, light cleaning only
├── intermediate/
│   └── int_invoices_joined.sql ← joins, deduplication, business logic
└── marts/
    └── mrt_billing_summary.sql ← final aggregates for BI consumption
```

```sql
-- sql/staging/stg_invoices.sql
-- Rename and cast only. No business logic here.
CREATE OR REPLACE VIEW staging.stg_invoices AS
SELECT
    inv_id                          AS invoice_id,
    cust_id                         AS customer_id,
    inv_dt::DATE                    AS invoice_date,
    inv_amt / 100.0                 AS invoice_amount_usd,
    UPPER(TRIM(status_cd))          AS status,
    _loaded_at                      AS loaded_at
FROM raw.invoices
WHERE inv_id IS NOT NULL;
```

```sql
-- sql/intermediate/int_invoices_joined.sql
-- Joins and business logic. References staging layer only.
CREATE OR REPLACE VIEW intermediate.int_invoices_joined AS
SELECT
    i.invoice_id,
    i.invoice_date,
    i.invoice_amount_usd,
    i.status,
    c.customer_name,
    c.customer_segment
FROM staging.stg_invoices      i
LEFT JOIN staging.stg_customers c USING (customer_id)
WHERE i.status != 'VOID';
```

```sql
-- sql/marts/mrt_billing_summary.sql
-- Final aggregates. What Tableau/Redshift consumers see.
CREATE OR REPLACE TABLE marts.mrt_billing_summary AS
SELECT
    DATE_TRUNC('month', invoice_date)   AS month,
    customer_segment,
    COUNT(*)                            AS invoice_count,
    SUM(invoice_amount_usd)             AS total_revenue_usd,
    AVG(invoice_amount_usd)             AS avg_invoice_usd
FROM intermediate.int_invoices_joined
GROUP BY 1, 2;
```

-----

### 4. Build a Python orchestration script with dependency logic

`Python` `Bash`

Chain your pipeline steps with explicit success/failure dependency checks. This is Airflow’s core concept — you’re building it manually first so that Airflow feels like an upgrade, not a new idea.

```python
import logging
import sys
from your_package.steps import ingest, stage, transform, export
from your_package.manifest import write_run_manifest

logger = logging.getLogger(__name__)

def run_pipeline(pipeline_name: str) -> None:
    steps = [
        ("ingest",    ingest.run),
        ("stage",     stage.run),
        ("transform", transform.run),
        ("export",    export.run),
    ]

    for step_name, step_fn in steps:
        logger.info(f"Starting step: {step_name}")
        try:
            result = step_fn()
            logger.info(f"Completed step: {step_name}", extra={"rows": result.get("rows")})
        except Exception as e:
            logger.error(f"Step failed: {step_name}", extra={"error": str(e)})
            write_run_manifest(pipeline_name=pipeline_name, status="failure", error=str(e), ...)
            sys.exit(1)

    write_run_manifest(pipeline_name=pipeline_name, status="success", ...)

if __name__ == "__main__":
    run_pipeline("billing_pipeline")
```

-----

### 5. Update your Selenium scrapers to land raw data to S3

`Selenium` `S3` `Python` `boto3`

Redirect scraper output from local files or Excel to S3 `raw/`. With your existing error handling already in place, this is mostly an output-destination swap.

```python
import json
import boto3
from selenium import webdriver
from your_package.logger import get_logger
from your_package.s3 import build_s3_key

logger = get_logger(__name__)

def scrape_and_land(bucket: str, source_name: str) -> str:
    driver = webdriver.Chrome()
    s3 = boto3.client("s3")
    records = []

    try:
        driver.get("https://portal.example.com/export")
        # ... your existing scrape logic ...
        records = [{"id": 1, "value": "example"}]  # replace with actual scrape
        logger.info("Scrape complete", extra={"records": len(records)})
    except Exception as e:
        logger.error("Scrape failed", extra={"error": str(e)})
        raise
    finally:
        driver.quit()

    # Land to S3 raw layer instead of writing to disk/Excel
    key = build_s3_key("raw", source_name, "json")
    s3.put_object(
        Bucket=bucket,
        Key=key,
        Body=json.dumps(records, default=str),
        ContentType="application/json"
    )
    logger.info("Landed to S3", extra={"bucket": bucket, "key": key})
    return key
```

**Goal:** A working layered pipeline: source → S3 raw → Snowflake staging → SQL transform → Redshift/S3 output. Built entirely with tools you own.

-----

## Phase 3 — Layer in dbt and Airflow

**Weeks 11–18 · Adopt DE-native tooling**

Because you’ve already built the patterns manually, these tools will feel like upgrades rather than new concepts.

-----

### 1. Install dbt-core and migrate your Snowflake SQL layers into dbt models

`dbt` `Snowflake` `VS Code` `Git`

Your Phase 2 SQL folder structure maps directly to dbt. Migration is mostly moving files and replacing hard-coded table references with `ref()`.

```bash
# Install and initialise
pip install dbt-snowflake
dbt init my_project
cd my_project
dbt debug   # verify Snowflake connection
```

```sql
-- models/staging/stg_invoices.sql
-- Same SQL as before, but dbt manages the CREATE/REPLACE
SELECT
    inv_id          AS invoice_id,
    cust_id         AS customer_id,
    inv_dt::DATE    AS invoice_date,
    inv_amt / 100.0 AS invoice_amount_usd,
    UPPER(TRIM(status_cd)) AS status
FROM {{ source('raw', 'invoices') }}
WHERE inv_id IS NOT NULL
```

```sql
-- models/intermediate/int_invoices_joined.sql
-- ref() replaces hard-coded schema.table references
SELECT
    i.invoice_id,
    i.invoice_date,
    i.invoice_amount_usd,
    c.customer_name,
    c.customer_segment
FROM {{ ref('stg_invoices') }}      i
LEFT JOIN {{ ref('stg_customers') }} c USING (customer_id)
WHERE i.status != 'VOID'
```

```bash
dbt run              # builds all models
dbt run -s stg_invoices   # builds one model
dbt docs generate && dbt docs serve   # auto-generated lineage docs
```

-----

### 2. Add dbt schema tests to your models

`dbt` `SQL`

Data quality tests require only YAML — no Python, no extra code. This is the highest-visibility DE skill most analyst-track candidates lack.

```yaml
# models/staging/schema.yml
version: 2

models:
  - name: stg_invoices
    description: "Cleaned and renamed invoice records from raw billing source."
    columns:
      - name: invoice_id
        description: "Primary key — unique identifier per invoice."
        tests:
          - not_null
          - unique

      - name: customer_id
        tests:
          - not_null
          - relationships:
              to: ref('stg_customers')
              field: customer_id

      - name: status
        tests:
          - accepted_values:
              values: ['PAID', 'PENDING', 'CANCELLED']
```

```bash
dbt test                        # run all tests
dbt test -s stg_invoices        # test one model
```

-----

### 3. Add dbt source freshness checks

`dbt` `SQL`

Beyond row-level tests, dbt can alert you when source data stops arriving — critical for production pipelines.

```yaml
# models/staging/sources.yml
version: 2

sources:
  - name: raw
    database: MY_SNOWFLAKE_DB
    schema: raw
    freshness:
      warn_after: {count: 6,  period: hour}
      error_after: {count: 24, period: hour}
    loaded_at_field: _loaded_at

    tables:
      - name: invoices
      - name: customers
```

```bash
dbt source freshness   # checks all sources against freshness thresholds
```

-----

### 4. Run Airflow locally via Docker and convert your orchestration script to a DAG

`Airflow` `Python` `Docker` `Bash`

Your Phase 2 orchestration script already has the dependency logic. Converting it to a DAG is mostly syntactic — Airflow adds scheduling, retries, alerting, and a UI on top.

```bash
# Spin up Airflow locally
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/stable/docker-compose.yaml'
docker compose up airflow-init
docker compose up
# UI available at http://localhost:8080
```

```python
# dags/billing_pipeline.py
from datetime import datetime, timedelta
from airflow.decorators import dag, task

@dag(
    schedule="0 6 * * *",          # daily at 06:00 UTC
    start_date=datetime(2025, 1, 1),
    catchup=False,
    default_args={
        "retries": 2,
        "retry_delay": timedelta(minutes=5),
        "owner": "data-engineering",
    },
    tags=["billing", "snowflake"],
)
def billing_pipeline():

    @task()
    def ingest():
        from your_package.steps.ingest import run
        return run()

    @task()
    def stage(ingest_result):
        from your_package.steps.stage import run
        return run()

    @task()
    def transform(stage_result):
        from your_package.steps.transform import run
        return run()

    @task()
    def export(transform_result):
        from your_package.steps.export import run
        return run()

    # Define dependency chain
    ingest_result    = ingest()
    stage_result     = stage(ingest_result)
    transform_result = transform(stage_result)
    export(transform_result)

billing_pipeline()
```

-----

### 5. Build a capstone DAG: Selenium → S3 → dbt → Redshift

`Airflow` `Selenium` `S3` `dbt` `Redshift`

Wire everything together. This is a complete, production-pattern DE pipeline and strong portfolio material.

```python
# dags/portal_to_redshift.py
from datetime import datetime, timedelta
from airflow.decorators import dag, task
from airflow.operators.bash import BashOperator

@dag(
    schedule="0 7 * * 1-5",        # weekdays at 07:00 UTC
    start_date=datetime(2025, 1, 1),
    catchup=False,
    default_args={"retries": 2, "retry_delay": timedelta(minutes=10)},
    tags=["portal", "selenium", "dbt"],
)
def portal_to_redshift():

    @task()
    def scrape_portal():
        """Selenium scraper → lands JSON to S3 raw/"""
        from your_package.scrapers.portal import scrape_and_land
        return scrape_and_land(bucket="my-data-bucket", source_name="billing_portal")

    @task()
    def load_raw_to_snowflake(s3_key: str):
        """Copy S3 raw file into Snowflake raw schema via COPY INTO"""
        from your_package.connectors import SnowflakeConnector
        sf = SnowflakeConnector()
        sf.execute_query(f"""
            COPY INTO raw.billing_portal
            FROM @my_s3_stage/{s3_key}
            FILE_FORMAT = (TYPE = JSON)
            ON_ERROR = ABORT_STATEMENT
        """)

    # dbt runs as a BashOperator — keeps dbt native CLI behaviour
    dbt_run = BashOperator(
        task_id="dbt_run",
        bash_command="cd /opt/dbt/my_project && dbt run --select billing_portal+ --profiles-dir .",
    )

    dbt_test = BashOperator(
        task_id="dbt_test",
        bash_command="cd /opt/dbt/my_project && dbt test --select billing_portal+ --profiles-dir .",
    )

    @task()
    def export_to_redshift():
        """Push dbt mart output from Snowflake to Redshift serving layer"""
        from your_package.steps.export import snowflake_to_redshift
        snowflake_to_redshift(
            source_table="marts.mrt_billing_summary",
            target_table="public.billing_summary"
        )

    # Wire the DAG
    s3_key = scrape_portal()
    load_raw_to_snowflake(s3_key) >> dbt_run >> dbt_test >> export_to_redshift()

portal_to_redshift()
```

**Goal:** A fully orchestrated, tested, documented pipeline. You’re doing DE work, not preparing to do it.

-----

## Phase 4 — Document, Share, and Position

**Ongoing · Make your work visible**

Engineering work that no one can see doesn’t advance your career.

-----

### 1. Publish your pipeline project to GitHub

`Git` `GitHub`

Write a README covering architecture, tools, and design decisions. Include a pipeline diagram. A suggested README structure:

```markdown
# billing-pipeline

## Architecture
[diagram: portal → S3 → Snowflake → dbt → Redshift → Tableau]

## Stack
- Ingestion: Python + Selenium + boto3
- Storage: AWS S3 (data lake), Snowflake (warehouse)
- Transformation: dbt-core (Snowflake)
- Orchestration: Apache Airflow
- Serving: Amazon Redshift → Tableau

## Project Structure
billing-pipeline/
├── dags/               # Airflow DAGs
├── dbt/                # dbt project (models, tests, docs)
├── your_package/       # shared Python package
│   ├── connectors/     # SnowflakeConnector, RedshiftConnector
│   ├── scrapers/       # Selenium scrapers
│   └── steps/          # pipeline step functions
├── config/             # env-based config
└── tests/              # unit tests

## Running Locally
...
```

-----

### 2. Replace at least one VBA macro with a Python pipeline

`Python` `VBA` `SQL`

Pick the most brittle or high-maintenance Excel macro and rebuild it using your existing package. Below is the structural pattern.

```python
# Before: VBA macro that queries Access/Excel and formats a report
# After: Python script using your existing package

import pandas as pd
from your_package.connectors import SnowflakeConnector
from your_package.exporters import export_to_excel, export_to_s3
from your_package.logger import get_logger

logger = get_logger(__name__)

def run_monthly_billing_report():
    sf = SnowflakeConnector()
    df = sf.execute_query("""
        SELECT * FROM marts.mrt_billing_summary
        WHERE month = DATE_TRUNC('month', CURRENT_DATE - INTERVAL '1 month')
    """)

    # Excel for stakeholders (matches what the macro produced)
    export_to_excel(df, filename="monthly_billing_report.xlsx")

    # S3 for the data layer
    export_to_s3(df, bucket="my-data-bucket", source_name="monthly_billing_report")

    logger.info("Monthly billing report complete", extra={"rows": len(df)})

if __name__ == "__main__":
    run_monthly_billing_report()
```

-----

### 3. Learn boto3 beyond basic uploads

`Python` `boto3` `S3`

Move from treating S3 as a file share to treating it as infrastructure.

```python
import boto3

s3 = boto3.client("s3")

# List all files in a prefix (e.g. check what landed today)
def list_raw_files(bucket: str, source: str, date_prefix: str) -> list:
    response = s3.list_objects_v2(Bucket=bucket, Prefix=f"raw/{source}/{date_prefix}/")
    return [obj["Key"] for obj in response.get("Contents", [])]

# Tag files with pipeline metadata for governance
def tag_s3_object(bucket: str, key: str, pipeline: str, status: str) -> None:
    s3.put_object_tagging(
        Bucket=bucket,
        Key=key,
        Tagging={"TagSet": [
            {"Key": "pipeline", "Value": pipeline},
            {"Key": "status",   "Value": status},
        ]}
    )

# Read a specific S3 file into a DataFrame without downloading it
def read_parquet_from_s3(bucket: str, key: str) -> pd.DataFrame:
    import pandas as pd
    from io import BytesIO
    obj = s3.get_object(Bucket=bucket, Key=key)
    return pd.read_parquet(BytesIO(obj["Body"].read()))
```

-----

### 4. Explore Redshift data modeling conventions

`SQL` `Redshift`

You query Redshift as a BI warehouse. Learn the engineering side — distribution and sort keys affect query performance significantly.

```sql
-- Distribution key: choose a column that's frequently used in JOINs
-- Sort key: choose a column that's frequently used in WHERE/ORDER BY
-- This prevents full table scans and reduces data shuffling across nodes

CREATE TABLE public.billing_summary (
    month               DATE         NOT NULL,
    customer_id         VARCHAR(50)  NOT NULL,
    customer_segment    VARCHAR(50),
    invoice_count       INTEGER,
    total_revenue_usd   DECIMAL(18,2),
    avg_invoice_usd     DECIMAL(18,2)
)
DISTKEY(customer_id)       -- rows with same customer_id land on same node
SORTKEY(month, customer_id); -- queries filtering by month scan less data

-- After bulk loads, always run these to maintain performance
VACUUM billing_summary;    -- reclaims space from deleted rows
ANALYZE billing_summary;   -- updates query planner statistics
```

**Goal:** A public portfolio, documented pipelines, and concrete modernization stories. You’re interviewing as a DE with receipts, not as an analyst hoping to transition.

-----

## The Core Insight

You’re not missing fundamentals — you already write code like an engineer. What’s left is **architecture and tooling**: structuring your work into formal pipeline layers, adopting dbt and Airflow to replace manual patterns you’ve already built, and making the work visible.

**Phase 1 can start today and is mostly additive to code you’ve already written.**
