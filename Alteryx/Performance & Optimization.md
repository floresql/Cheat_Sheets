# Alteryx — Performance & Optimization Cheat Sheet

## 1. Streamline Your Data (Early & Often)
*   **Filter Early:** Use a **Filter tool** as close to the input as possible to reduce the number of records flowing downstream.
*   **Drop Fields:** Use a **Select tool** (or the embedded select in Join/Spatial tools) to remove unnecessary columns.
*   **Smallest Data Types:** Use the **Auto Field tool** to automatically assign the most efficient data types (e.g., converting a String to a Int16 if the numbers fit).

## 2. Speed Up Development
*   **Cache and Run:** Right-click a tool and select **Cache and Run Workflow**. This freezes the data at that point, so Alteryx doesn't have to re-process the beginning of the workflow every time you run it.
*   **Record Limits:** In the **Input Data tool** configuration, set a "Record Limit" (e.g., 1000) during development so you aren't waiting for millions of rows to load.
*   **Disable Browse Tools:** Browse tools are resource-intensive. When your workflow is stable, go to **Canvas > Runtime > Disable All Browse Tools**.

## 3. Tool Choice Matters
*   **Avoid Data Cleansing Tool:** For large datasets, the **Data Cleansing tool** is a slow macro. Use a **Formula tool** with `TRIM()` or `REGEX_REPLACE()` for much faster results.
*   **In-Database (In-DB):** For massive database datasets, use **In-DB tools** to push the processing logic to the database server instead of pulling all data into your local RAM.
*   **AMP Engine:** Ensure **AMP (Alteryx Multi-threaded Processing)** is enabled in your Workflow Runtime settings to utilize all your CPU cores.
