# Alteryx — Troubleshooting & Error Handling

## 1. Common Errors
*   **"Field Not Found":** Usually caused by a **Select tool** or **Join tool** upstream that dropped or renamed a column.
*   **"Type Mismatch":** You are trying to perform math on a String or a Join on two different data types (e.g., String to V_String).
*   **"Truncated Data":** Your string field length (e.g., 255) is too short for the incoming data. Use **Auto Field** or manually increase size.

## 2. Debugging Steps
*   **Browse Everywhere:** Add a Browse tool after a tool that is behaving unexpectedly to see exactly what the data looks like at that point.
*   **Test Tool:** Use the **Test Tool** to set "Rules." If a rule is broken (e.g., "Column A should never be Null"), the workflow will throw an error and stop.
*   **Message Tool:** Configure the **Message Tool** to report how many records pass a certain point in the log.
