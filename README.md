========================
PROMPT 1 — SPLIT UI INTO TWO TABS: "Editor" and "Executions"
========================
TASK
Refactor the Workflow Creator screen into two top-level tabs:
- Editor
- Executions

STRICT RULES
- DO NOT change business logic.
- DO NOT change bot execution code.
- DO NOT change drag/drop or node connection logic.
- DO NOT change how logs are produced today.
- Only change UI layout, view composition, and styling.

REQUIREMENTS
1) Replace the current "Design / Execution" toggle with a centered segmented tab control like:
   [ Editor ] [ Executions ]
   (match the rounded pill style from the provided screenshot: selected tab is white, unselected is gray)
2) Tabs must switch the screen content completely:
   - Editor tab shows: Available Bots (left) + Canvas (center) + Validate (top-right or top bar)
   - Executions tab shows: Execution list + Execution details/console (no bot library, no canvas editing)
3) Keep all existing state and handlers intact; just render different layouts based on selected tab.

DELIVERABLE
- Unified diff only
- List changed files at the top


========================
PROMPT 2 — EDITOR TAB LAYOUT (DESIGN EXPERIENCE ONLY)
========================
TASK
Implement the "Editor" tab layout to focus purely on designing the workflow.

STRICT RULES
- No changes to logic, only UI.
- Keep drag/drop working exactly the same.

EDITOR TAB MUST SHOW
LEFT: "Available Bots" panel (existing)
CENTER: Canvas (existing)
TOP BAR (right aligned or within header row): actions for design only:
- Validate
- Clear

REMOVE FROM EDITOR TAB
- Any execution console/output drawer
- Any "Running step" indicator
- Any live execution text

CANVAS FRAME
- Add a visible border around canvas container:
  border: 1px solid #D6D9DE
  border-radius: 12px
  background: #F8FAFC
  subtle shadow

VALIDATE BEHAVIOR (UI only)
- Validate should show results on canvas (badges/outline) or a small "Validation" drawer.
- Do not run actual bot execution during validate.

DELIVERABLE
- Unified diff only


========================
PROMPT 3 — EXECUTIONS TAB LAYOUT (RUN EXPERIENCE ONLY)
========================
TASK
Implement the "Executions" tab layout so execution is completely separate from design.

STRICT RULES
- DO NOT change how bots run today (bat execution remains).
- DO NOT change execution ordering, scheduling, or runner code.
- Only display execution details using existing captured output/log data.

EXECUTIONS TAB MUST SHOW
A) Top area: small toolbar (right aligned)
- Run (primary)
- Stop (only if already exists; otherwise omit)
- Clear (optional)

B) Left side: Execution History list (or "Current Execution" if you only have one)
Each row/card shows:
- Execution timestamp / id
- Status (Running/Success/Failed)
- Duration
- Step count (e.g., 2/5)

C) Right side: Execution Detail panel
When user selects an execution, show per-bot steps:
- Bot name
- Status
- Exit code
- Duration
- Expandable stdout/stderr (or log text)
- Log path if available

REMOVE FROM EXECUTIONS TAB
- Available Bots panel
- Drag/drop editor UX
- Any design validation UI

OPTIONAL (recommended)
- Keep a read-only mini "flow preview" at top (tiny breadcrumb of bot names) but NO canvas editing.

DELIVERABLE
- Unified diff only


========================
PROMPT 4 — STYLE MATCH: FINTECH SEGMENTED TABS (LIKE SCREENSHOT)
========================
TASK
Restyle the Editor/Executions tab switch to match the provided reference screenshot.

STRICT RULES
- CSS/styling only; no logic changes.

STYLE SPEC
- Segmented control container: light gray background (#EEF2F7), rounded 12px, padding 4px
- Tab buttons: height 36px, min width 110px, border-radius 10px
- Selected tab: white background, subtle shadow, darker text
- Unselected tab: transparent background, muted text
- Place the segmented control centered at the top of the canvas area (or centered in the header row)

Also improve overall typography slightly:
- Section titles: 14–15px semibold
- Body text: 12–13px
- Muted helper text: #6B7280

DELIVERABLE
- Unified diff only



========================
PROMPT 1 — EXECUTION VIEW MUST LOOK LIKE A CONSOLE (TERMINAL UI)
========================
TASK
Restyle the Execution window to look like a terminal console.

STRICT RULES
- DO NOT change bot execution logic.
- DO NOT change how .bat or runner.py is invoked.
- DO NOT change business logic.
- Only UI rendering + CSS.

REQUIREMENTS
1) The execution output area must look like a console:
   - dark background (terminal-style)
   - monospace font (Consolas / Menlo / monospace fallback)
   - line spacing ~1.4
   - wrap long lines (no horizontal scrolling by default)
   - auto-scroll to bottom while running (if already implemented, keep it)
2) Add a subtle top bar inside the console region:
   - title: "Console"
   - small status indicator: Running / Completed / Failed (use existing state if present; otherwise omit)
3) The console area must support:
   - Copy button (copies visible console text)
   - Clear console button (clears UI buffer only; does not change execution)

DELIVERABLE
- Unified diff only.
- Use existing styling approach in repo (no new libraries).
- Ensure readability and spacing.

========================
PROMPT 2 — FILTER OUTPUT: SHOW ONLY runner.py “STEPS”, HIDE COMMANDS
========================
TASK
Filter execution output so the UI shows only meaningful step lines coming from runner.py, not shell commands.

STRICT RULES
- DO NOT change the .bat content.
- DO NOT change runner.py.
- DO NOT change the process runner.
- Only filter what is DISPLAYED in the UI.

DISPLAY RULES (IMPORTANT)
Show lines that match ANY of the below (keep original order):
A) Timestamped lines:
   - starts with "[" + time like [19:34:47]
B) Step keywords (case-insensitive):
   - PRE-CONDITION:
   - CONDITION:
   - STEP:
   - ACTION:
   - RESULT:
   - ERROR:
   - WARNING:
   - Target:
   - FLOW-
   - [Driver]
C) Any line that begins with "===" or "----" used as separators

HIDE lines that match ANY of the below (case-insensitive):
- starts with "(venv)" or contains "\.venv\"
- starts with "C:\\" prompt style output like "C:\Users\..."
- contains "setlocal" or "endlocal"
- contains "echo off" or "echo "
- contains "set BASE=" or other environment variable setup
- contains "python.exe" invocation lines that echo the command
- any bare command plumbing that does not include the keywords in DISPLAY RULES

IMPLEMENTATION GUIDANCE
- Add a UI-level function like `shouldShowConsoleLine(line: string): boolean`
- Filter the buffered output before rendering.
- Keep a toggle “Show raw output” (collapsed/hidden by default) only if easy; otherwise skip.

DELIVERABLE
- Unified diff only.
- Confirm in comments the filtering is UI-only and does not affect execution.

========================
PROMPT 3 — EXECUTION STEPS VIEW: GROUP BY BOT + COLLAPSIBLE STEP SECTIONS
========================
TASK
Improve the Execution tab so output is presented as step groups per bot, not as a flat dump.

STRICT RULES
- Do not change execution logic.
- Do not change runner.py.
- UI-only grouping of already captured console lines.

REQUIREMENTS
1) For each bot execution, show a collapsible panel:
   - Header: Bot Name + status badge (Running/Success/Failed)
   - Small metadata: duration + exit code (if already available)
2) Inside each bot panel, render the console output (already filtered from Prompt 2) in console style.
3) Add a “Steps only” mode (default ON):
   - If ON: show only lines with step keywords (PRE-CONDITION/STEP/ACTION/RESULT/ERROR/WARNING/Target/FLOW/[Driver])
   - If OFF: show all lines that passed the DISPLAY RULES filter from Prompt 2
4) Make the console readable:
   - preserve indentation
   - allow selecting text
   - show newest lines at bottom
   - keep auto-scroll while running

DELIVERABLE
- Unified diff only.
- No new dependencies.




