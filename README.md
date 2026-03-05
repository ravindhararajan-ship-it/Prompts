========================
PROMPT 1 — FIX TOP ROW ALIGNMENT (TABS + TOOLBAR SAME ROW)
========================
TASK
Align the Editor/Executions segmented tabs and the toolbar actions into the same single header row.

STRICT RULES
- Do not change business logic.
- UI layout/CSS only.

REQUIREMENTS
1) Create a single header row container above the canvas area.
2) Left/Center: Segmented control tabs: [Editor] [Executions]
3) Right: Action buttons (contextual based on active tab)
4) Tabs and buttons must be vertically aligned (same baseline) with consistent spacing.
5) Remove any extra spacing/margins that cause toolbar to drop to another row.

LAYOUT SPEC
- Header row: display:flex; align-items:center; justify-content:space-between;
- Tabs container: flex:0 0 auto;
- Actions container: flex:0 0 auto; display:flex; gap:10px;

DELIVERABLE
- Unified diff only
- List changed files


========================
PROMPT 2 — REMOVE VALIDATE COMPLETELY (BUTTON + VALIDATION SECTION)
========================
TASK
Remove Validate button and remove the Validation section/panel from the Editor tab entirely.

STRICT RULES
- Do not change workflow logic.
- If validate handler exists, keep it but do not render any UI that triggers it.
- UI-only removal.

REQUIREMENTS
1) Remove/hide Validate button everywhere.
2) Remove/hide the Validation section (“Run Validate…”, status, etc.) everywhere.
3) Reclaim vertical space: canvas expands to fill.
4) Ensure no empty container remains.

DELIVERABLE
- Unified diff only
- List changed files


========================
PROMPT 3 — EXECUTIONS TAB: SHOW CANVAS + ONE WINDOWS-CONSOLE FOR ALL OUTPUT
========================
TASK
Redesign the Executions tab to:
- show the workflow canvas (read-only OK)
- show ONE combined console output for the entire run
- remove "Current Execution" panel
- remove per-bot sections/collapsibles
- console must look like Windows cmd.exe

STRICT RULES
- DO NOT change bot execution logic (.bat/runner.py).
- DO NOT change process invocation.
- Only change UI rendering of output.

REQUIREMENTS (EXECUTIONS TAB)
A) Layout
- Top: Canvas panel (same canvas component; editing disabled is fine)
- Bottom: Console panel (full width)
- No left/right split for execution metadata.
- Remove “Current Execution” table entirely.
- No separate sections per bot.

B) Console Appearance (Windows cmd)
- background: #0C0C0C (near-black)
- text color: #CCCCCC
- font-family: Consolas, "Lucida Console", monospace
- font-size: 12px (small)
- line-height: 1.35
- hard edges: border-radius: 4px (minimal) or 0 if you prefer cmd style
- subtle border: 1px solid #2B2B2B
- padding: 10px
- selectable text, copyable
- auto-scroll to bottom while running (keep existing if already present)

C) Controls (top-right of console header, compact)
- Steps only toggle (default ON)
- Copy button
- Clear button
- Run button stays in the main header row (right aligned), not floating inside console unless already implemented.

D) Output filtering (display only)
- Steps only ON: show meaningful runner.py lines (timestamps and step keywords)
- Hide command noise (venv, echo, setlocal, python.exe invocation, C:\ prompt lines)
- IMPORTANT: Filtering is UI-only; raw output still available internally.

DELIVERABLE
- Unified diff only
- List changed files
- Confirm: “Executions tab shows canvas + single combined console”
