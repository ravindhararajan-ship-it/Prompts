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
No explanation.
