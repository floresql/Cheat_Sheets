# Best Practices - Visual & Performance.md

Combining visual design best practices with high-performance SQL data modeling to create fast, insightful dashboards.

---

## 1. Dashboard Design & Layout
*   **The 5-Second Rule:** Users should grasp the main KPI within five seconds.
*   **Hierarchy (F-Pattern):** Place high-level KPIs in the **top-left** corner (natural scanning pattern).
*   **BANs (Big Angry Numbers):** Use large, bold summary metrics at the top for immediate headlines.
*   **Limit Views:** Stick to **2–4 worksheets** per dashboard to avoid overcrowding.
*   **Fixed Sizing:** Use **fixed-size layouts** instead of "Automatic" so Tableau can reuse cached layouts.

## 2. SQL Efficiency (The "Golden Rules")
Tableau is metadata-heavy; every extra column adds "weight."
*   **Never use `SELECT *`**: Only pull the columns needed for the dashboard.
*   **Filter in the `WHERE` Clause**: Filter as close to the source as possible.
*   **Avoid `ORDER BY`**: Tableau has its own sorting engine; don't make the DB do it twice.
*   **Custom SQL vs. Views**: 
    *   **Database Views (High Performance):** Recommended; pre-calculated logic handled by the DB.
    *   **Custom SQL (Low Performance):** Avoid; Tableau wraps these in subqueries that can bypass DB indexes.
*   **Union All:** Use `UNION ALL` instead of `UNION` to avoid the slow distinct-check process.

## 3. Data Architecture & Aggregation
*   **Aggregate at the Source:** If showing Monthly Sales, don't pull 100M raw rows. Aggregate in SQL first:
    ```sql
    -- FAST: Aggregating in SQL to reduce row count
    SELECT DATE_TRUNC('month', transaction_date) as sale_month,
           store_id, SUM(sale_amount) as total_sales
    FROM sales_table GROUP BY 1, 2;
    ```
*   **Extracts over Live:** Use **Extracts (.hyper)** for faster querying and calculation materialization.
*   **Hide Unused Fields:** Use "Hide All Unused Fields" in the Data Pane to shrink the extract size.
*   **Join Optimization:** Join on **Integers** (IDs) rather than Strings. Use Tableau "Relationships" (Noodles) for Join Culling.

## 4. Visual Clarity & Tooltips
*   **Maximize Data-Ink:** Remove "chartjunk" (heavy borders, dark grid lines).
*   **Color with Purpose:** Use neutral bases (gray/white) and limit palettes to **under 5 colors**.
*   **Simplify Tooltips:** Rewrite tooltips into clear sentences (e.g., "The total sales for [Region] were [Sales]").

## 5. Calculation & Filter Performance
*   **Data Types:** Use **Booleans or Integers** in calculations/filters; they are significantly faster than Strings.
*   **Filter Efficiency:** 
    *   Use **Extract/Data Source Filters** to limit data before it hits the workbook.
    *   Use **Context Filters** (gray filters) to force Tableau to filter data before LODs are calculated.
*   **Complex Logic:** Push logic to the **database level** (SQL/ETL) whenever possible.
*   **Avoid ATTR:** Use `MIN` or `MAX` instead of `ATTR` or `AVG` to reduce computation load.

## 6. Interactivity & Advanced Techniques
*   **Filter Actions:** Use Dashboard Actions instead of "Quick Filter" dropdowns for faster rendering.
*   **Common Table Expressions (CTEs):** Use CTEs in your views for readability and better execution plans.
*   **Handling Distinct Counts:** `COUNT(DISTINCT)` is expensive. Pre-calculate flags in SQL:
    ```sql
    -- Create a unique flag in a View to avoid overhead
    SELECT user_id, MIN(transaction_date) OVER(PARTITION BY user_id) as first_purchase
    FROM sales;
    ```

## 7. Quick Development Shortcuts


| Action | Shortcut (Windows) | Shortcut (Mac) |
| :--- | :--- | :--- |
| **New Worksheet** | `Ctrl + M` | `Cmd + T` |
| **Swap Rows/Columns** | `Ctrl + W` | `Ctrl + Cmd + W` |
| **Undo / Redo** | `Ctrl + Z` / `Y` | `Cmd + Z` / `Shift + Z` |
| **Show Me Menu** | `Ctrl + 1` | `Cmd + 1` |
| **Clear Worksheet** | `Alt + Shift + Backspace` | `Opt + Shift + Delete` |


## 8. Visualization & Communication
*   **Know Your Audience:** 
    *   **Executives:** Need "The Bottom Line" (High-level KPIs, clear trends).
    *   **Managers:** Need "The Driver" (Why is this happening?).
    *   **Operators:** Need "The Action" (List of accounts to call, specific items to fix).
*   **The "So What?":** Every chart should have a headline that explains the takeaway (e.g., instead of "Monthly Revenue," use "Revenue Increased 15% due to Holiday Promo").
*   **Color Theory:** Use color to highlight the *exception*, not just to make it pretty.

