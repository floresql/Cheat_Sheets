# Tableau Cheat Sheet: Advanced Calculations

### 1. Level of Detail (LOD) Expressions
LODs allow you to calculate values independent of the dimensions in your current view.
*   **FIXED:** Ignores view dimensions (except Context Filters).
    ```sql
    { FIXED [Region] : SUM([Sales]) }
    ```
*   **INCLUDE:** Adds a dimension to the calculation even if it isn't in the view.
    ```sql
    { INCLUDE [Customer Name] : AVG([Sales]) }
    ```
*   **EXCLUDE:** Removes a dimension from the calculation for that specific metric.
    ```sql
    { EXCLUDE [Category] : SUM([Sales]) }
    ```

### 2. Handling Nulls (ZN & IFNULL)
Ensure your calculations don't break when data is missing.
*   **ZN:** Converts a null value to zero.
    ```sql
    ZN([Sales]) + ZN([Profit])
    ```
*   **IFNULL:** Replaces a null with a specific value or string.
    ```sql
    IFNULL([Member Name], "Unknown")
    ```

### 3. Ad-Hoc Calculations
*   **The Trick:** Double-click any empty space on the **Rows**, **Columns**, or **Marks** shelf to type a formula directly (e.g., `SUM([Sales]) * 1.1`) without creating a named field in the data pane.


### 4. Ranking Functions
Tableau offers different ways to rank data; choosing the right one matters for ties.
*   **RANK:** Standard (1, 2, 2, 4).
*   **RANK_DENSE:** No gaps (1, 2, 2, 3).
*   **RANK_UNIQUE:** Forces a unique rank even if values are identical (1, 2, 3, 4).
    ```sql
    RANK(SUM([Sales]), 'desc')
    ```

### 5. Window Functions (Moving Averages)
Used to "smooth out" volatile data trends.
*   **Moving Average:** Calculates the average of the current row and a specified number of previous/following rows.
    ```sql
    // Average of the last 6 months
    WINDOW_AVG(SUM([Sales]), -6, 0)
    ```

### 6. Lookup & Offset (YoY/MoM)
Access values from other rows in the view without using complex joins.
*   **LOOKUP:** Grab a value from a previous period.
    ```sql
    // Difference from previous month
    SUM([Sales]) - LOOKUP(SUM([Sales]), -1)
    ```

### 7. Running Totals
*   **RUNNING_SUM:** Accumulates values across the view (e.g., "Pacing toward goal").
    ```sql
    RUNNING_SUM(SUM([Sales]))
    ```
