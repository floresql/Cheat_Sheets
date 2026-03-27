# Alteryx — Workflow Organization & Documentation

## 1. Visual Organization
*   **Tool Containers:** Group related tools into a **Tool Container**. You can label them (e.g., "Step 1: Input & Cleanse") and **Disable** them to stop that specific branch from running.
*   **Comment Boxes:** Use the **Comment tool** to add large text blocks or even images to explain the business logic behind a section.
*   **Annotations:** Rename tool annotations (the text under the tool icon) to describe what that specific tool is doing (e.g., "Filter for Active Customers").

## 2. Best Practice Checklist
*   [ ] **Select Tool at Input:** Immediately following an Input tool, use a Select tool to set names and types.
*   [ ] **Uncheck "Unknown":** In your final Select/Join tools, uncheck the **\*Unknown** box to prevent unexpected new columns from breaking your output schema.
*   [ ] **Alignment:** Highlight tools and use **Ctrl + Shift + -** (Horizontal) or **Ctrl + Shift + +** (Vertical) to snap them into neat lines.
