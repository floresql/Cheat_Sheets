# Web-based Analytics Retrieval Pipeline (WARPzone)

**WARPzone** is a modular `Python` automation package for data exports from web-based reporting systems using `Selenium`.

It is designed to support:

- Multiple download jobs
- Multiple report URLs
- Shared browser automation logic
- Per-job configuration via YAML
- Environment-based runtime settings

---

## Project Structure

```text
WARPzone/
├── .env
├── .gitignore
├── pyproject.toml
├── README.md
├── config/
│   └── jobs.yaml
├── data/
│   └── raw/
├── src/
│   └── warpzone/
│       ├── __init__.py
│       ├── main.py
│       ├── settings.py
│       ├── models.py
│       ├── job_loader.py
│       ├── logging_config.py
│       ├── selenium_runner.py
│       └── workflows/
│           ├── __init__.py
│           ├── base.py
│           └── microstrategy_export.py
└── tests/
    └── __init__.py