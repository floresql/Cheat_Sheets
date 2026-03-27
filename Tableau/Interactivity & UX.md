# Tableau Cheat Sheet: Interactivity & UX

### 1. Parameter-Driven Sheet Swapping
Switch between different charts in the same dashboard container.
1.  Create a **String Parameter** (e.g., "Select View").
2.  Create a calculation: `[Select View] = "Map"`.
3.  Place the calculation on the **Filters** shelf of the map sheet and select **True**.
4.  Place sheets in a **Vertical Container** on the dashboard and hide titles.

### 2. Viz in Tooltip
Show a secondary chart when a user hovers over a data point.
1.  Create the secondary worksheet (the "target").
2.  In the main worksheet, click **Tooltip** in the Marks card.
3.  Click **Insert** > **Sheets** > Select your target sheet.
4.  Adjust `maxwidth` and `maxheight` in the generated string.

### 3. Dynamic Titles & Tooltips
Inject user selections directly into text.
*   **How:** In the "Edit Title" or "Tooltip" dialog, click **Insert** in the top right.
*   **Selection:** Choose a **Parameter** or **Field** to make the text update live (e.g., "Sales for <Region>").

### 4. Parameter Actions (One-Click Updates)
Make your dashboard feel like an app by allowing users to click a mark to change a parameter value.
*   **How:** Dashboard > **Actions** > **Add Action** > **Change Parameter**.
*   **Use Case:** Click a "Year" bar to update a "Trend" line chart for that specific year.
