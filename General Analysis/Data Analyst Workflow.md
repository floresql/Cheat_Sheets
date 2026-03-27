# Data Analyst Project Workflow

## 1. Project Scoping & Objectives
- [ ] **Define the Problem:** What business question are we answering?
- [ ] **Identify Stakeholders:** Who will use this data and what is their "definition of done"?
- [ ] **Establish Metrics:** Define key performance indicators (KPIs) and success criteria.
- [ ] **Resource Check:** Confirm access to necessary databases, APIs, or files.

## 2. Data Collection & Extraction
- [ ] **Identify Sources:** Locate internal databases, third-party APIs, or flat files (CSV, Excel).
- [ ] **Raw Data Backup:** Always keep an untouched version of the original data.
- [ ] **Environment Setup:** Initialize your Git repository and project directory structure.

## 3. Data Cleaning & Preprocessing
- [ ] **Remove Duplicates:** Identify and delete identical or nearly identical rows.
- [ ] **Handle Missing Values:** Decide whether to drop rows, impute values (mean/median), or flag them.
- [ ] **Fix Structural Errors:** Correct typos, inconsistent capitalization, and mislabeled categories.
- [ ] **Format Data Types:** Ensure dates are `datetime` objects and numeric strings are floats/integers.
- [ ] **Filter Outliers:** Identify and investigate anomalies that could skew results.

## 4. Exploratory Data Analysis (EDA)
- [ ] **Summary Statistics:** Calculate mean, median, mode, and standard deviation for key variables.
- [ ] **Distribution Analysis:** Use histograms or box plots to visualize data spread.
- [ ] **Correlation Checks:** Identify relationships between different variables.
- [ ] **Data Profiling:** Document data volume, variety, and velocity.

## 5. Analysis & Modeling
- [ ] **Feature Engineering:** Create new variables (e.g., "Customer Lifetime Value" from transaction history).
- [ ] **Perform Core Analysis:** Run the specific queries or models needed to answer the project's primary questions.
- [ ] **Validate Results:** Cross-reference findings against known benchmarks or historical data.

## 6. Visualization & Reporting
- [ ] **Choose the Medium:** Decide between a static report (PDF), interactive dashboard (Tableau/Power BI), or slide deck.
- [ ] **Simplify Visuals:** Ensure every chart has a clear title, labeled axes, and answers a specific question.
- [ ] **Draft Recommendations:** Translate data findings into actionable business advice.

## 7. Documentation & Final Delivery
- [ ] **Update README:** Document the data lineage, cleaning steps, and how to run the code.
- [ ] **Refine Code:** Clean up comments and ensure the analysis is reproducible.
- [ ] **Stakeholder Handover:** Present findings and gather feedback for potential iteration.
