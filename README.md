Update the left sidebar UX.

Do NOT change workflow logic.
Do NOT refactor architecture.
Only update sidebar rendering + bot_library.json schema + filter UI.

Requirements:

1) Rename
- Rename sidebar title from "BOT Library" to "Collection".

2) Data model (JSON-driven)
- Update bot_library.json so each item includes:
  - id
  - display_name
  - short_description
  - type  // "BOT" or "API" (required)
  - category (optional)
  - inputs[] (optional)
  - outputs[] (optional)

3) Two content types
- The Collection must show both BOT and API items, mixed in one list by default.

4) Type label next to title
- Each item must show a small label next to display_name:
  - text: BOT or API
  - rendered as small “pill/superscript” chip (compact, rounded)
  - style must be subtle and clean (not loud)
  - chip color differs slightly for BOT vs API
- The label must come from item.type in JSON (no hardcoding).

5) Filter control (3-way switch)
- Add a neat segmented control at top of sidebar with 3 options:
  - ALL | BOT | API
- Default selection: ALL
- Clicking filters the list instantly (no reload).
- Selected segment must look clearly active, but minimal.

6) Visual design
- Must match app styling (same fonts, spacing, rounded corners).
- Compact rows, clean hierarchy.
- Keep the existing badge/initial style if already implemented, but ensure it doesn’t conflict with the new type chip.

Output:
- Updated bot_library.json example (include both BOT and API items)
- Code changes to load JSON type field
- Sidebar UI changes (title rename + segmented control + type chip + filtering)

  -------------------

  Implement this by editing the actual code files (no pseudo).

Task: Redesign Field Mapping popup UI and mapping model.

Rules:
- Do NOT refactor architecture.
- Do NOT change connection creation behavior.
- Only update mapping UI + mapping data storage + JSON persistence.
- Modify existing files in-place. Create new files only if required.

You MUST:
1) Identify files responsible for:
   - connector click / yellow handle click
   - field mapping popup UI
   - edge/connection model persistence (save/load workflow JSON)
   - bot_library.json loading (inputs/outputs)
2) Update those files directly.

UI requirements:
- Open popup ONLY when clicking the small yellow square mapping handle.
- Popup is macOS-style (no Windows controls look).
- Top: two headers only: [Source BOT Name] [Target BOT Name]
- Below: mapping rows with dropdowns:
   Left dropdown = Source fields = SourceBot.outputs[] + EXTRA option "Excel Input"
   Right dropdown = Target fields = TargetBot.inputs[]
- Add Row button + delete row per mapping.
- Save persists: edge.mappings = [{source:"Excel Input|<output>", target:"<input>"}]
- Save/load workflow JSON must persist mappings.

Output:
- List files changed with exact paths.
- Provide final code changes (diff or full file content).
- Update bot_library.json schema if required.
- No explanations.

- -----------------------

Implement this by editing the actual code files (no pseudo).

Task: Sidebar title becomes "Collection". Sidebar renders BOTH BOT and API items from bot_library.json. Each item shows a small solid chip label "BOT" or "API" next to title. Add 3-way solid segmented switch: ALL | BOT | API.

Rules:
- Do NOT refactor architecture.
- Do NOT change workflow logic.
- Only update sidebar UI + styling + JSON-driven data fields.
- Modify existing files in-place. Create new files only if required.

You MUST:
1) Identify files responsible for:
   - sidebar rendering / list items
   - sidebar header area
   - filter UI controls
   - bot_library.json schema + loader
2) Update those files directly.

Requirements:
- bot_library.json includes item.type = "BOT" | "API" (required).
- Collection list shows all when ALL selected; filters instantly for BOT/API.
- Filter control must use SOLID backgrounds, colorful but fintech-light palette.
- Chip label next to title must be SOLID background, different for BOT vs API.
- Styling must match app (rounded, clean, minimal; no Windows default look).

Output:
- List files changed with exact paths.
- Provide final code changes (diff or full file content).
- Provide updated bot_library.json example.
- No explanations.

- ----------------

Implement this by editing the actual code files (no pseudo).

Task: Toolbar buttons (Zoom In, Zoom Out, Clear Canvas, Generate Input Template, Generate Standalone Application) must be aligned to the RIGHT and styled like n8n: light toolbar, rounded buttons, soft hover, subtle divider.

Rules:
- Do NOT change button actions or handlers.
- Do NOT refactor architecture.
- Only adjust toolbar layout + styling.
- Modify existing files in-place.

You MUST:
1) Identify the file(s) that define:
   - toolbar layout container
   - button creation/styling
2) Update those files directly.

Requirements:
- Right align all toolbar buttons as a group.
- Light solid toolbar background + subtle bottom border.
- Buttons: rounded, light solid backgrounds, soft hover, no harsh borders.
- Fintech-light palette only.

Output:
- List files changed with exact paths.
- Provide final code changes (diff or full file content).
- No explanations.
No explanation.
