## Project Organization

```
Report_Builder/
│
├── README.md                   <- The top-level README for developers using this project.
├── reference                   <- Data dictionaries, manuals, and all other explanatory materials.
├── reports/                    <- Individual reports are stored here.  
│   └── Report_Name/            <- Each report gets a folder with content specific to that report.
│       ├── data/                  
│       │   ├── external/       <- Data from third party sources, e.g. FOA.
│       │   ├── processed/      <- The final, canonical data sets for reporting.
│       │   └── raw/            <- The original, immutable data dump.    
│       │                       
│       ├── email/              <- Holds files and script needed to email the report(s) 
│       ├── logs/               <- Project run and error logs.
│       ├── macros/             <- Scripts to turn processed data into report files 
│       ├── Report_Name.xlsx    <- The finished report product.
│       ├── run.bat             <- One batch run them all.
│       └── sql/                <- Drop SQL file(s) in, main.py runs query for each file in the folder       
│           └── sql file(s)        for each of three schemas, and outputs Excel file. 
│
├── src/                        <- Source code for use in this project — where the magic happens.
│   ├── __pycache__/            <- Python generate to store compiled bytecode to speed up the startup 
│   │   └── pyc file(s)            time for subsequent runs and module imports. 
│   │
│   ├── __init__.py             <- Makes src a Python module
│   ├── config.py               <- Stores useful variables and configuration
│   ├── excel_export.py         <- Exports query results to excel in processed data folder.
│   ├── external_data.py        <- Scripts to get data from external sources, e.g. FOA, BI
│   ├── main.py                 <- Main entry point, contains execution flow
│   └── snowflake_handler.py    <- SnowflakeSQLRunner class and related logic to connect to Snowflake
│
├── .env                        <- Environment variables file.
└── requirements.txt            <- Reproduce environment with `pip install -r requirements.txt`

```

