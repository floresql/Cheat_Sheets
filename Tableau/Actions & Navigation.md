# Tableau Cheat Sheet: Actions & Navigation

### 1. URL Actions with Values
Send users to a specific website or another tool, passing data through the URL.
*   **The Format:** `https://google.com<Customer Name>`
*   **How:** Dashboard > **Actions** > **Go to URL**. When a user clicks a customer, it opens a Google search for them automatically.

### 2. Highlight Actions
Help users find related data points across different charts without filtering out the rest of the context.
*   **Pro Tip:** Use "Selected Fields" in the Highlight Action menu to only highlight a specific dimension (like `Product Category`) while ignoring others.

### 3. Set Actions (Asymmetric Drilling)
Allow users to click a mark to "expand" it into more detail while leaving other marks collapsed.
1.  Create a **Set** based on a dimension (e.g., `Category Set`).
2.  Create a calculation: `IF [Category Set] THEN [Sub-Category] ELSE "" END`.
3.  Add a **Dashboard Action** to "Update Set Values" on click.
