Update the UI so the "Editor" and "Executions" tabs appear exactly like a segmented control inside the Title Bar (similar to modern workflow tools like n8n).

Requirements:
1. Place the Editor / Executions control inside the Title Bar, horizontally centered.
2. The control must be vertically centered within the Title Bar height.
3. The control should look like a segmented toggle:
   - rounded pill container
   - light gray background
   - thin border
4. Each tab (Editor, Executions) must be smaller in height than the Title Bar.
5. Active tab:
   - white background
   - subtle shadow or border
   - darker text
6. Inactive tab:
   - transparent background
   - lighter gray text
7. Tabs must visually appear as part of one control (no spacing between them).
8. Clicking the tab must only switch UI mode (Editor / Executions) without modifying any existing workflow logic.
9. Do NOT modify any business logic, workflow execution logic, or API calls — only update layout and styling.
10. Ensure the component is responsive and remains centered even when the window resizes.

Expected result:
The Title Bar shows a centered segmented toggle with two options:
[ Editor ] [ Executions ]
where the selected tab is clearly highlighted.
