========================
PROMPT 1 — EDITOR TAB: FIX AVAILABLE BOTS (NO SCROLLBAR, N8N STYLE)
========================
TASK
Update the Editor tab left sidebar ("Available Bots") to match n8n node picker style and remove visible scrollbars.

STRICT RULES
- DO NOT change business logic.
- DO NOT change drag/drop behavior.
- UI and CSS only.

REQUIREMENTS
1) Sidebar layout
- Title: "Available Bots"
- Subtitle: "Drag bots onto canvas to build workflow"
- Search input styled like n8n (rounded, subtle border)
2) Bot list must be scrollable but with NO visible scrollbar:
- keep scrolling working (mouse wheel / trackpad)
- hide scrollbar using CSS (platform safe):
  - for webkit: ::-webkit-scrollbar { width: 0; height: 0; }
  - for firefox: scrollbar-width: none;
3) Bot cards n8n style:
- white cards on light gray background
- hover highlight (slight blue border or background tint)
- compact padding, good typography
- no huge empty spaces
4) Ensure there is no “weird bottom scroll bar” on the bot panel.
5) Keep the existing drag/drop bindings exactly as-is.

DELIVERABLE
- Unified diff only
- List changed files


========================
PROMPT 2 — EDITOR TAB: REMOVE VALIDATION COMPLETELY (SECTION + BUTTON)
========================
TASK
Remove validation UI from the Editor tab entirely.

STRICT RULES
- Do not change backend/business logic.
- If Validate handler exists, keep it in code but remove/hide UI triggers.
- UI-only removal.

REQUIREMENTS
1) Remove/hide:
- Validate button
- Validation section/drawer/panel
- “Run Validate to view…” text
2) Reclaim the space:
- Canvas should expand vertically to fill that space.
3) Do not leave empty containers.

DELIVERABLE
- Unified diff only
- List changed files


========================
PROMPT 3 — N8N CANVAS LOOK: GRID + FRAME + DEPTH (EDITOR + EXECUTIONS)
========================
TASK
Make the canvas look like n8n: dotted grid background + framed panel + subtle depth. Apply to both Editor and Executions (if canvas appears there too).

STRICT RULES
- No node logic changes.
- No handle/connector logic changes.
- CSS only (or className adjustments).

REQUIREMENTS
1) Canvas container frame:
- background: #F8FAFC
- border: 1px solid #D6D9DE
- border-radius: 12px
- subtle shadow: 0 1px 3px rgba(0,0,0,0.08)
2) Grid:
- dotted or light grid pattern similar to n8n
- very subtle dots/lines (do not overpower)
3) Empty state hint (Editor only, if no nodes):
- centered light text: “Drag a bot here to start”
- disappears once a node exists

DELIVERABLE
- Unified diff only
- List changed files


========================
PROMPT 4 — EXECUTIONS TAB: SHOW CANVAS + COMBINED EXECUTION PANEL + REAL CONSOLE UI (SMALL FONT)
========================
TASK
Redesign the Executions tab to look like n8n:
- keep a canvas preview at top (read-only is fine)
- combine “Current Execution” and “Execution Details” into one unified execution panel
- console-style output with small monospace font and dark background
- show steps only (runner.py meaningful lines) and hide command noise

STRICT RULES
- DO NOT change bot execution logic (.bat / runner.py).
- DO NOT change ordering or runner behavior.
- Only display/format captured output.

LAYOUT REQUIREMENTS (n8n-like)
TOP: Canvas preview (same nodes/edges, no editing required)
BOTTOM: Execution panel (single panel, no split empty columns)

EXECUTION PANEL CONTENT
- Header: “Execution”
- Inline run controls on right:
  - Run (primary)
  - Steps only (toggle, default ON)
  - Copy
  - Clear
- Body: console output region

CONSOLE STYLE
- Background: #0B1220 (or similar deep navy/black)
- Text: #E5E7EB
- Font: monospace (Consolas/Menlo)
- Font size: 12px (small, dense)
- Line height: 1.35–1.45
- Wrap long lines
- Auto-scroll while running

OUTPUT FILTERING (UI ONLY)
Show only runner.py step lines:
- timestamp lines like [19:34:47]
- keywords: PRE-CONDITION, STEP, ACTION, RESULT, ERROR, WARNING, Target, FLOW-, [Driver]
Hide command plumbing:
- (venv), setlocal/endlocal, echo off, python.exe command lines, C:\ prompt lines, env var setup

DELIVERABLE
- Unified diff only
- List changed files
