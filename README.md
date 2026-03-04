========================
PROMPT 1 — REMOVE RIGHT BOT DETAILS + CLEAN HEADER
========================
TASK
Update the workflow screen to REMOVE the right-side "BOT DETAILS" inspector panel completely and reclaim the space for the canvas.

STRICT RULES (DO NOT BREAK)
- DO NOT modify any business logic.
- DO NOT modify workflow execution logic.
- DO NOT modify drag/drop or node connection logic.
- DO NOT modify API calls, data models, JSON generation.
- Only UI layout / styling changes.

REQUIREMENTS
1) Remove the entire right panel (BOT DETAILS / inspector section).
2) The center canvas must expand to use the newly freed space.
3) Remove the “Workflow Builder” header title section and remove “Active” + “Save” controls from the top area.
   - If those buttons are wired to business logic, do NOT delete handlers; just hide the UI elements.
4) Keep the left “Available Bots” panel unchanged and visible.
5) Ensure the UI still renders and the canvas interactions work exactly as before.

DELIVERABLE
- Provide unified diff only.
- List changed files at the top.


========================
PROMPT 2 — FINTECH COMMAND BAR (REPLACE BORING BOTTOM TOOLBAR)
========================
TASK
Replace the bottom toolbar (Validate Flow / Run Workflow / View Flow JSON / Clear Canvas) with a top-right fintech-style command bar.

STRICT RULES
- Reuse existing button handlers exactly as-is.
- Do not change any backend calls or logic.
- Do not rename actions or state fields.
- UI-only restructuring + styling.

REQUIREMENTS
1) Remove or hide the entire bottom toolbar container.
2) Add a compact command bar anchored at the top-right of the canvas area (inside the main content container).
3) Buttons (reuse existing actions/handlers):
   - + Add (optional: opens existing “add bot” flow if present; if not present, omit this button)
   - Validate
   - Run (primary)
   - View JSON
   - Export (if exists; otherwise omit)
   - Clear

VISUAL STYLE (FinTech)
- Button height 32–36px
- Compact spacing, subtle shadows
- Primary button: “Run ▷” (filled)
- Secondary buttons: outline/ghost
- Use a clean palette:
  Background: #F5F7FA
  Border: #D6D9DE
  Primary: #1D4ED8 (or existing primary)
  Text: #111827
  Muted: #6B7280
- Command bar container:
  white background, border, radius 10px, slight shadow, looks like an enterprise toolbar.

DELIVERABLE
- Unified diff only.
- Do not introduce new libraries.
- Use the existing styling mechanism used in the repo.


========================
PROMPT 3 — MAKE IT FEEL “ALIVE”: STATUS STRIP + CANVAS VISUALS
========================
TASK
Make the UI feel more enterprise/fintech by adding a lightweight status strip and improving canvas density WITHOUT touching logic.

STRICT RULES
- No logic changes.
- No API changes.
- No new data models.
- Styling + layout only.

REQUIREMENTS
1) Add a small status strip near the command bar (top-right area), showing:
   - Status: Draft / Validated / Running / Completed (use existing status state if present; if not, show “Draft” static label)
   - Last run: (if existing runtime state exists; otherwise show “—”)
2) Improve canvas background:
   - light grid or dotted grid (very subtle)
   - reduce the “empty” feel by adding a soft vignette or slight center emphasis (CSS-only, optional)
3) Node styling improvements (CSS/classnames only):
   - better contrast
   - small header line inside node
   - selected node has stronger border glow
   - keep ports/handles unchanged
4) Left “Available Bots” panel:
   - slightly stronger card borders
   - hover effect
   - keep drag behavior unchanged

DELIVERABLE
- Unified diff only.
- Confirm in comments which elements were hidden vs removed.
