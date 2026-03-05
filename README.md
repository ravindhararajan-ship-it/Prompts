UI THEME REVERT — BACK TO FINTECH (LIGHT, CLEAN, ENTERPRISE)

GOAL
Revert the app from the dark/colorful theme back to a fintech-style light theme:
- Light background
- Neutral grays
- Blue accent
- Subtle borders + shadows
Keep current layout (Bot Library panel, canvas grid, run-in-canvas/clear-in-canvas) unchanged.

STRICT RULES
- CSS/theme only. Do NOT change any business logic.
- Do NOT change drag/drop logic, execution logic, polling logic, or data structures.
- Keep existing components; only update styling.

------------------------------------------------------------
STEP 1 — DEFINE FINTECH THEME VARIABLES (ROOT)
Replace current theme variables with:

--bg: #F6F8FB
--panel: #FFFFFF
--panel-2: #F9FAFB
--surface: #FFFFFF
--text: #111827
--muted: #6B7280
--border: #E5E7EB
--shadow: 0 8px 20px rgba(17,24,39,0.08)
--shadow-soft: 0 3px 10px rgba(17,24,39,0.06)

Primary/Accent (fintech blue):
--primary: #1D4ED8
--primaryHover: #1E40AF
--focusRing: rgba(29,78,216,0.20)

Success:
--success: #16A34A
Warning:
--warning: #F59E0B
Danger:
--danger: #DC2626

Remove any heavy gradients on the app background.

------------------------------------------------------------
STEP 2 — APP BACKGROUND (LIGHT)
Set main app background to:
background: var(--bg);

Remove:
- radial gradients
- dark overlays
- vignette layers (if added earlier)

------------------------------------------------------------
STEP 3 — TOP TITLE BAR + EDITOR/EXECUTIONS TOGGLE (FINTECH)
Top bar:
- background: #FFFFFF
- border-bottom: 1px solid var(--border)
- height: 52px
- display flex, center the toggle
- z-index above canvas

Segmented toggle (Editor/Executions):
- background: #F3F4F6
- border: 1px solid #E5E7EB
- height: 28px
- font-size: 12px
- border-radius: 8px (allowed only for toggle)
Active tab:
- background: #FFFFFF
- text: var(--text)
- subtle shadow: 0 1px 2px rgba(0,0,0,0.06)
Inactive:
- text: #6B7280
- hover: background #EEF2FF

Ensure toggle is fully visible (no clipping):
- header overflow: visible
- parent overflow: visible
- toggle container: -webkit-app-region: no-drag if Electron

------------------------------------------------------------
STEP 4 — LEFT BOT LIBRARY PANEL (LIGHT FINTECH)
Sidebar:
- background: var(--panel)
- border-right: 1px solid var(--border)
- padding: 16px
- no dark tints

Header "BOT LIBRARY (2)":
- font-size 12px
- font-weight 700
- letter-spacing 0.06em
- color #374151

Search input:
- background #FFFFFF
- border 1px solid #D1D5DB
- height 32px
- border-radius 8px
- focus ring: 0 0 0 3px var(--focusRing)

Bot cards:
- background #FFFFFF
- border 1px solid #E5E7EB
- border-radius 10px
- box-shadow: 0 1px 2px rgba(0,0,0,0.05)
Hover:
- border-color: rgba(29,78,216,0.35)
- box-shadow: 0 8px 18px rgba(17,24,39,0.08)
Selected:
- outline or left bar using --primary (not neon)
Left accent bar:
- width 4px, background: --primary for both bots (fintech consistent)

Remove emoji icons if present; use a small subtle circle or monochrome icon instead.

------------------------------------------------------------
STEP 5 — CANVAS (LIGHT + VISIBLE GRID)
Canvas container:
- background: #FFFFFF
- border: 1px solid var(--border)
- box-shadow: var(--shadow-soft)
- border-radius: 10px (allowed)
- remove any dark vignette overlays

Grid (clear but subtle):
background-color: #FFFFFF;
background-image:
  linear-gradient(to right, rgba(17,24,39,0.08) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(17,24,39,0.08) 1px, transparent 1px),
  linear-gradient(to right, rgba(17,24,39,0.04) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(17,24,39,0.04) 1px, transparent 1px);
background-size:
  120px 120px,
  120px 120px,
  24px 24px,
  24px 24px;

------------------------------------------------------------
STEP 6 — CANVAS NODES (FINTECH)
Node cards:
- background: #FFFFFF
- border: 1px solid #E5E7EB
- border-radius: 12px
- box-shadow: 0 10px 24px rgba(17,24,39,0.10)
Title: #111827, weight 600
Labels: #6B7280
Ports: --primary with subtle ring (no glow)
Hover:
- border-color: rgba(29,78,216,0.40)

------------------------------------------------------------
STEP 7 — RUN/CLEAR BUTTONS INSIDE CANVAS (CLEAN)
Run button (in Executions canvas):
- background: var(--primary)
- hover: var(--primaryHover)
- border-radius: 0 or 8px (choose ONE style globally; recommended 8px for fintech consistency)
- shadow: 0 8px 18px rgba(17,24,39,0.12)

Clear button (bottom-right inside canvas):
- background: #DC2626
- hover: #B91C1C
- border-radius consistent with Run
- keep visible only when nodes exist (if already implemented)

------------------------------------------------------------
STEP 8 — REMOVE DARK THEME ARTIFACTS
Search and remove/override any styles that set:
- background: #0b1220 / #0f172a / dark rgba overlays
- text: #e5e7eb
- heavy neon borders
- vignette ::after overlays

------------------------------------------------------------
DELIVERABLE
Return:
1) unified diff only
2) files modified
3) confirm: light fintech theme restored, layout unchanged, logic untouched
