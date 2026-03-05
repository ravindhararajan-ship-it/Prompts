========================
PROMPT 1 — CANVAS FRAME + REMOVE STATUS BAR + REMOVE VIEW JSON
========================
TASK
UI-only fixes:
1) Add a clear border/frame around the canvas area (like a fintech app panel).
2) Remove the Status/Draft/Last run bar completely.
3) Remove the "View JSON" button from the command bar.

STRICT RULES
- DO NOT modify business logic.
- DO NOT modify workflow execution logic.
- DO NOT modify drag/drop or node connections.
- ONLY modify layout + styling + button visibility.
- If any removed control is wired to logic, do NOT delete handlers; hide UI elements instead.

CANVAS FRAME SPEC
- Canvas container background: #F8FAFC
- Border: 1px solid #D6D9DE
- Border radius: 12px
- Subtle shadow: 0 1px 3px rgba(0,0,0,0.08)
- Ensure the canvas fills container and does not overflow.

DELIVERABLE
- Unified diff only.
- List changed files at the top.


========================
PROMPT 2 — ADD MODE SWITCH: DESIGN vs EXECUTION
========================
TASK
Introduce a two-mode UI switch: "Design" and "Execution" in the top-right command area.

STRICT RULES
- Do not alter existing handlers for Validate/Run/Clear.
- Do not change backend logic.
- UI state only for mode selection.

REQUIREMENTS
1) Add segmented control: [Design] [Execution]
2) In Design mode: show buttons -> Validate, Clear
3) In Execution mode: show buttons -> Run, (Stop if existing), Clear
4) Remove any status labels. No "Draft/Last run".

Implementation guidance:
- Mode can be a local UI state variable.
- Buttons must call existing handlers unchanged.

DELIVERABLE
- Unified diff only.


========================
PROMPT 3 — VALIDATE SHOULD LINT/SIMULATE + ANNOTATE CANVAS (CODE-STYLE VALIDATION)
========================
TASK
Transform "Validate" into a design-time validation experience:
- Validate should simulate/lint the workflow and display results directly on the canvas and in a bottom "Validation" drawer.

STRICT RULES
- Do NOT run real bot execution in Validate.
- Do not change existing workflow execution logic.
- You may add NEW UI-only validation functions that analyze the already-available workflow graph/state.
- Do not change existing data models; only read them.

REQUIREMENTS
A) Validation checks (minimum):
- Node disconnected
- Missing required input fields (if metadata exists)
- Missing required mapping from upstream outputs to downstream inputs
- Cycles (if your system forbids)
- Missing script/bat path (if this metadata exists)
B) Canvas annotations:
- Add small badges on nodes: ✅ ⚠️ ❌ based on validation result
- Highlight edges/nodes with errors (red border) or warnings (yellow)
- Hover tooltip shows error message(s)
C) Bottom drawer:
- Create a collapsible bottom drawer titled "Validation"
- Show a list like IDE problems:
  - severity (Error/Warning)
  - message
  - node name
- Clicking an item focuses/highlights the node on the canvas.

NO "View JSON".
Validation output must be visual + drawer list, not modal.

DELIVERABLE
- Unified diff only.
- Include a short note in comments explaining where validation reads workflow state from.


========================
PROMPT 4 — EXECUTION MODE: SHOW REAL BOT RUN OUTPUT (BAT FILE TELEMETRY) IN EXECUTION DRAWER
========================
TASK
In Execution mode, show execution details for each bot run in a bottom "Execution" drawer instead of toolbar status.

STRICT RULES
- Do NOT change how bots run today (each bot runs a .bat file).
- Do NOT change business logic, ordering, or execution.
- ONLY add UI plumbing to DISPLAY execution details that already exist OR can be captured from existing process invocation outputs.
- If execution currently captures stdout/stderr/exit code internally, bind UI to those existing fields.
- If execution currently writes to log files, read/display those log paths and tail content (UI-side) using existing functions; do not change bot behavior.

REQUIREMENTS
A) Execution Drawer UI
- Title: "Execution"
- Table/list per node:
  - Bot name
  - Status: Queued/Running/Success/Failed
  - Duration
  - Exit code
  - Expandable "Output" (stdout/stderr)
  - Log path (if available)

B) Canvas execution overlay (Execution mode only)
- During run, show running spinner or blue glow on active node
- After run, show ✅/❌ on each node

C) Switching modes
- Design mode shows Validation drawer
- Execution mode shows Execution drawer
- Only one drawer visible at a time

DELIVERABLE
- Unified diff only.
- If you need a small adapter interface, create it in UI layer only and do not modify bot runner logic.
