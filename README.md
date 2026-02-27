Modify the existing canvas node/card rendering code files (real code changes, not pseudo).

Goal (Canvas):
- Show ONLY the BOT/API display_name on each node.
- Remove/hide ALL “Input:” and “Output:” lines from node cards.

Hyperlink behavior:
- The node name must behave like a hyperlink:
  - pointer cursor on hover
  - underline on hover
  - clickable

On click:
- Clicking the node name opens a compact macOS-style modal popup (no Windows look).
- Popup content must be loaded from bot_library.json using the node’s id:
  - display_name
  - type (BOT/API)
  - short_description
  - inputs[] (if present)
  - outputs[] (if present)

UI style (macOS):
- Rounded corners (12px)
- Light background (#ffffff)
- Soft shadow
- Minimal title bar (or custom header)
- Clean spacing + modern fonts
- No default Windows borders/widgets visible

You MUST:
1) Update the actual canvas rendering file to remove input/output text and render name-only.
2) Update the click/hover handler file to implement hyperlink interactions.
3) Update/ensure bot_library.json loader/lookup function exists and is used.
4) Add/modify the popup component in the real UI files.

Output required:
- List the exact file paths modified
- Provide final updated code (diff or full file content)
- No explanation
