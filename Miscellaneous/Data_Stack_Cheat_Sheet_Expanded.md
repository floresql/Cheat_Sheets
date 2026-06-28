# Modern Data Stack — Cheat Sheet (Expanded)

> Tags used throughout: **[TS]** = table stakes (expected at any level), **[DIFF]** = differentiator (signals Senior/Lead/Principal readiness)

---

## 1. Languages

| Language | Role | Notes |
|---|---|---|
| **SQL** | [TS] | Non-negotiable at every level. Window functions, CTEs, query optimization separate mid from senior. |
| **Python** | [TS]→[DIFF] | Pandas is table stakes. PySpark, SQLAlchemy, packaging your own modules/CLI tools is what differentiates DE from DA. |
| **Bash** | [TS] | Cron, file ops, piping — assumed baseline for anyone touching Linux-based pipelines. |
| **Scala/Java** | [DIFF] (niche) | Only matters in Spark-native shops where JVM performance is prioritized over PySpark overhead. Don't prioritize unless job posts in your target market ask for it. |

**Trade-off:** Going deep on Python (OOP, testing, packaging) generally pays off more than breadth across languages — most DE job postings filter on Python + SQL, not language count.

---

## 2. Cloud Providers

| Provider | Where it dominates | Signature services |
|---|---|---|
| **AWS** | Largest overall market share, most DE job postings | S3, Redshift, Glue, Kinesis, Lambda |
| **Azure** | Enterprises already on Microsoft stack | ADLS, Synapse, Data Factory, Event Hubs |
| **Google Cloud** | ML-heavy orgs, BigQuery shops | BigQuery, Dataflow, Pub/Sub, Vertex AI |

**Recommendation:** Don't spread thin across all three. Pick the one most common in your target job postings (for most U.S. DE roles, that's AWS) and go deep — IAM, networking basics, cost awareness, not just the data services.

---

## 3. Storage & Compute: Warehouse vs. Lake vs. Lakehouse

| Pattern | What it is | Examples | Best for |
|---|---|---|---|
| **Data Warehouse** | Structured, schema-on-write, optimized for SQL analytics | Snowflake, Redshift, BigQuery | BI, reporting, structured analytics |
| **Data Lake** | Raw object storage, schema-on-read, cheap at scale | S3, ADLS, GCS | Landing zone, unstructured/semi-structured data |
| **Lakehouse** | Lake storage + warehouse-like transactions/performance | Databricks (Delta Lake), Snowflake/Iceberg | Unifying BI + ML workloads on one copy of data |

**[DIFF]** Open table formats (**Delta Lake**, **Apache Iceberg**, **Hudi**) are increasingly an ATS keyword and interview topic for senior DE roles — they solve the "one copy of data, multiple compute engines" problem. Warehouse-only experience is becoming [TS]; lakehouse/open-table-format fluency is the differentiator.

---

## 4. Ingestion

| Approach | Tools | Notes |
|---|---|---|
| **Batch** | Python scripts, Fivetran, Airbyte, SQLAlchemy/API pulls | Most common entry point for analysts moving into DE |
| **Streaming** | Kafka, AWS Kinesis, GCP Pub/Sub | Needed for near-real-time use cases (fraud detection, live dashboards) |
| **CDC (Change Data Capture)** | Debezium, Fivetran CDC connectors | Captures row-level changes from source DBs without full reloads |

**Recommendation:** You likely already have strong batch ingestion chops (Selenium scraping, SQLAlchemy/Snowflake pulls). The differentiator is showing you understand *when* CDC or streaming is the right call versus full/batch refresh — that's a senior-level architectural decision, not just a tool choice.

---

## 5. Transformation

- **ETL vs. ELT:** Cloud warehouse compute made ELT (load raw, transform in-warehouse) the dominant pattern — transformation logic lives close to the data instead of in a separate ETL server.
- **dbt** — [TS]→[DIFF] boundary tool. Basic dbt models are increasingly expected; testing, macros, exposures, and the **dbt Semantic Layer** are what show senior maturity.
- **Spark / PySpark** — [DIFF]. Needed once data volume exceeds what a single-node warehouse query can handle efficiently, or for unstructured/ML-adjacent transformation.

**Trade-off:** dbt and Spark aren't competitors — dbt handles SQL-based, warehouse-native transformation; Spark handles distributed, code-native transformation at scale. Senior candidates should be able to articulate *which one and why* for a given workload, not just "I know both."

---

## 6. Orchestration

| Tool | Style | Market position |
|---|---|---|
| **Apache Airflow** | DAG-based, code-as-config | Industry standard — most job postings, most legacy footprint |
| **Prefect** | Pythonic, dynamic workflows, easier local dev | Growing in startups; signals modern awareness |
| **Dagster** | Asset-based (data-aware, not just task-aware), strong lineage | Growing in data-platform-maturity orgs |

**Recommendation:** Airflow is the safe, high-leverage choice to go deep on — it's the most common ATS keyword and most likely to match what you'll inherit at a new job. Knowing *of* Prefect/Dagster and being able to speak to trade-offs (asset-aware orchestration vs. task-aware) is enough to signal currency without needing production depth in all three.

---

## 7. Data Modeling

- **Normalized vs. Denormalized** — core trade-off: normalization reduces redundancy and write anomalies (good for OLTP); denormalization trades storage for read speed (good for OLAP/analytics).
- **Modeling philosophies:**
  - **Kimball (dimensional modeling)** — star schemas, fact/dimension tables, optimized for BI. Most common in practice.
  - **Inmon (normalized EDW)** — fully normalized enterprise warehouse, dimensional marts built downstream.
  - **Data Vault** — hub/link/satellite structure, built for auditability and rapid schema change in large enterprises.
- **Star vs. Snowflake schema:** star = denormalized dimensions (simpler joins, more storage); snowflake = normalized dimensions (less redundancy, more joins).

**[DIFF]** Being able to explain *why* you'd choose Kimball over Data Vault for a given org's maturity level is a senior/lead-level conversation — most candidates can only describe what a star schema is, not when to deviate from it.

---

## 8. Database Choice: OLTP vs. OLAP

| Type | Schema | Storage | Use Case | Examples | Why |
|---|---|---|---|---|---|
| **OLTP** | Normalized | Row-store | Apps / backend transactions | PostgreSQL, MySQL, SQL Server, Oracle | Fast individual reads/writes/updates/deletes |
| **OLAP** | Denormalized | Column-store | Analytics, reporting | Snowflake, Redshift, BigQuery, Databricks, DuckDB | Fast scanning/aggregating across millions of rows |

**Why column-store matters:** OLAP engines read only the columns a query touches instead of full rows, which is *the* core reason analytical queries on column-stores outperform row-stores at scale — a good interview talking point if asked "why not just run analytics on Postgres?"

---

## 9. Architecture Patterns

| Pattern | Structure | Best for |
|---|---|---|
| **Medallion (Bronze/Silver/Gold)** | Bronze = raw, Silver = cleaned/validated, Gold = business-ready/star schema | Lakehouse-style ELT pipelines; popularized by Databricks but tool-agnostic |
| **Lambda Architecture** | Separate batch layer + speed (streaming) layer, merged at serving | Use cases needing both historical accuracy and low-latency views |
| **Kappa Architecture** | Streaming-only, batch treated as replay of the stream | Simpler ops than Lambda; used when near-real-time is the default, not the exception |

**Recommendation:** Medallion is the most directly applicable to your current pipeline work and the easiest to map onto resume bullets. Lambda/Kappa are worth knowing conceptually for system-design interview questions even if you haven't implemented them.

---

## 10. BI / Serving Layer

| Tool | Notes |
|---|---|
| **Tableau** | Strong on flexible, exploratory visualization; widely used in enterprise |
| **Power BI** | Dominant in Microsoft-centric orgs; tighter Excel/Azure integration |
| **Looker** | LookML semantic layer — governance-first, "define once, reuse everywhere" |
| **Metabase** | Lightweight, common in smaller/startup orgs |

**[DIFF]** Semantic layers (**dbt Semantic Layer**, **Cube**, LookML) decouple business logic from any one BI tool — increasingly a senior/lead talking point since it solves "every dashboard tool has a different definition of revenue."

---

## 11. Version Control & DevOps for Data

- **Git** — [TS]. Branching, PRs, merge conflict resolution; you already operate a dual-remote/bare-repo GitLab setup, which is above baseline.
- **CI/CD for pipelines** — GitHub Actions, GitLab CI — automated testing/deployment of dbt models, Airflow DAGs, etc.
- **Infrastructure as Code** — **Terraform** is the big one. [DIFF] — frequently listed in senior DE job descriptions, rarely possessed by analysts transitioning into DE. Strong ROI if you're targeting Principal-track roles.

---

## 12. Data Quality & Observability

- **In-pipeline testing:** dbt tests (`unique`, `not_null`, `relationships`), Great Expectations for more complex validation.
- **Observability platforms:** Monte Carlo, Bigeye, Databand — monitor freshness, volume, schema drift in production pipelines.

**[DIFF]** At senior/lead level, the expectation shifts from "my pipeline works" to "I have automated detection for when it silently breaks." This is a strong resume differentiator if you've built any freshness/anomaly checks, even informally.

---

## 13. Governance & Security

- **Cataloging/lineage:** Alation, Atlan, dbt docs/lineage graphs.
- **Access control & PII handling:** row/column-level security, masking policies (Snowflake has native support for both).
- **Lineage tracking:** increasingly expected so teams can answer "what breaks downstream if I change this column?"

---

## 14. Roles Mapped to the Stack

| Role | Primarily touches |
|---|---|
| **Data Analyst** | SQL, BI tools, light Python, gold-layer tables |
| **Data Engineer** | Ingestion, transformation, orchestration, storage architecture, IaC |
| **Data Scientist** | Modeling, statistics, Python/ML libraries, feature stores |
| **AI/ML Engineer** | Model deployment, MLOps, vector stores, serving infrastructure |

---

## 15. Gap Check Against Your Current Stack

Based on what you've already built (SQL, Python, Selenium, SQLAlchemy, Snowflake, S3, Parquet, DuckDB, Tableau, Alteryx, SQL Server, GitLab):

| You have | Status | Watch for |
|---|---|---|
| SQL, Python, Snowflake, S3, Parquet, DuckDB | Solid [TS] foundation | — |
| Tableau, Alteryx | Solid serving-layer coverage | — |
| GitLab (dual-remote/bare-repo workflow) | Above [TS] | — |
| **Orchestration (Airflow/Prefect/dbt)** | **Gap** | Increasingly a [TS] keyword for Senior DA / DE postings — highest-leverage next skill |
| **Open table formats (Iceberg/Delta)** | **Gap** | [DIFF] — strong if targeting lakehouse-forward orgs |
| **Infrastructure as Code (Terraform)** | **Gap** | [DIFF] — common ask at senior+ DE level |
| **Data observability (tests/monitoring)** | **Partial gap** | Worth surfacing any existing validation work explicitly on your resume |

This list is a good candidate for a phased learning roadmap (near/mid/long-term) if you want to turn it into a study plan next.
