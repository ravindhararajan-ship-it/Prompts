UI UPDATE — EXECUTIONS TAB: MOVE RUN INTO CANVAS + STRONGER GRID + NO ROUNDED CORNERS

GOAL
- In the Executions tab, move the Run button from the header into the canvas, bottom-right overlay.
- Make the canvas grid clearly visible (n8n-like).
- Remove rounded corners from canvas container and overlays.

STRICT RULES
- DO NOT change workflow execution logic.
- DO NOT change run handler behavior; only relocate the existing Run button.
- UI/CSS only.

------------------------------------------------------------
A) MOVE RUN BUTTON INTO CANVAS (EXECUTIONS TAB ONLY)

1) Locate the Executions tab header area where "Run" button is currently rendered.
   - Remove/hide Run button from the header in Executions tab view.

2) In the Executions tab canvas container (the wrapper that contains the workflow diagram/canvas),
   add a bottom-right overlay container inside the canvas:

CanvasWrapper (position: relative)
  CanvasSurface
  RunOverlay (position: absolute; bottom-right)

3) Render the existing Run button inside RunOverlay ONLY when the active tab is Executions.
   - Reuse the same onClick handler/function currently used by Run.
   - Do not change button label or handler.

RunOverlay CSS requirements:
- position: absolute;
- right: 16px;
- bottom: 16px;
- z-index: 60;

Run button styling requirements:
- background: #2563EB (fintech blue)
- color: #FFFFFF
- border: 1px solid #1D4ED8
- border-radius: 0 (no rounded corners)
- padding: 8px 14px
- font-size: 12px
- font-weight: 600
- box-shadow: 0 1px 2px rgba(0,0,0,0.12)
Hover:
- background: #1D4ED8

Optional (recommended):
- Disable button while running (if you already have running state) but do NOT add new logic; only bind to existing running flag if present.

------------------------------------------------------------
B) MAKE GRID CLEARLY VISIBLE (CANVAS BACKGROUND)

1) Locate the canvas background styling (the element showing the large white area).
2) Replace plain white background with a visible grid using CSS background layers.

Grid requirements:
- Light background (#FFFFFF or #FAFBFD)
- Two-level grid (minor + major lines) like n8n
- Must remain visible at normal zoom and not overpower nodes

Apply to CanvasSurface CSS:

background-color: #FFFFFF;
background-image:
  linear-gradient(to right, rgba(15,23,42,0.08) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(15,23,42,0.08) 1px, transparent 1px),
  linear-gradient(to right, rgba(15,23,42,0.04) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(15,23,42,0.04) 1px, transparent 1px);
background-size:
  120px 120px,
  120px 120px,
  24px 24px,
  24px 24px;
background-position: 0 0, 0 0, 0 0, 0 0;

(If the canvas library already has a grid option, prefer turning that on instead of CSS, but only if it’s trivial and doesn’t affect behavior.)

------------------------------------------------------------
C) REMOVE ROUNDED CORNERS (CANVAS + OVERLAYS)

1) Identify canvas container/frame styles that use border-radius.
2) Set border-radius: 0 for:
- Canvas frame/container
- Canvas inner surface wrapper
- RunOverlay container (if it has any radius)
- Any canvas toolbars shown inside canvas

Also ensure the canvas has a clear border:
border: 1px solid #D0D5DD;

------------------------------------------------------------
DELIVERABLE

Return:
1) Unified diff only
2) Files modified
3) Confirm:
   - Run button removed from header in Executions tab
   - Run button appears bottom-right inside canvas
   - Grid is visible and two-level
   - No rounded corners on canvas/frame/overlay
  

UI POLISH PASS — MAKE THE APP LOOK LIKE A FINISHED COLORFUL PRODUCT (NO LOGIC CHANGES)

GOAL
Make the UI feel like a polished standard workflow tool: colorful accents, layered surfaces, clear hierarchy, modern shadows, better canvas background, and strong hover/selected states.

STRICT RULES
- DO NOT change business logic, execution logic, drag/drop logic, or data structures.
- Styling + layout polish only (CSS + small markup wrappers OK).

THEME (DEFINE CSS VARIABLES ONCE)
Create a theme palette (non-fintech, colorful) using CSS variables at app root:

--bg: #0b1220
--panel: #0f172a
--panel-2: #111c33
--surface: #0c152b
--text: #e5e7eb
--muted: #94a3b8
--border: rgba(255,255,255,0.10)
--shadow: 0 10px 30px rgba(0,0,0,0.35)
--shadow-soft: 0 6px 18px rgba(0,0,0,0.25)

Accent gradient:
--accentA: #7c3aed
--accentB: #22c55e
--accentC: #06b6d4
--accentD: #f97316

Primary button:
--primary: #7c3aed
--primaryHover: #6d28d9

Danger:
--danger: #ef4444

STEP 1 — APP BACKGROUND (REMOVE PLAIN WHITE)
Set the main app background to a subtle gradient so it feels premium:
background: radial-gradient(1200px 700px at 20% 10%, rgba(124,58,237,0.25), transparent 55%),
            radial-gradient(900px 600px at 80% 20%, rgba(6,182,212,0.18), transparent 55%),
            radial-gradient(900px 600px at 30% 90%, rgba(34,197,94,0.14), transparent 60%),
            var(--bg);

STEP 2 — LEFT SIDEBAR "BOT LIBRARY" (MAKE IT LOOK LIKE A TOOL)
- Sidebar background: var(--panel)
- Border-right: 1px solid var(--border)
- Add a top mini header strip with subtle gradient and icon:
  header background: linear-gradient(90deg, rgba(124,58,237,0.20), rgba(6,182,212,0.10));
- Make BOT LIBRARY title white, count muted.
- Search input:
  background: rgba(255,255,255,0.06)
  border: 1px solid rgba(255,255,255,0.10)
  color: var(--text)
  placeholder: rgba(229,231,235,0.45)
  focus ring: 0 0 0 3px rgba(124,58,237,0.35)

Bot cards:
- background: rgba(255,255,255,0.06)
- border: 1px solid rgba(255,255,255,0.10)
- shadow: 0 4px 12px rgba(0,0,0,0.20)
- On hover: translateY(-1px), border color rgba(124,58,237,0.55), background slightly brighter
- Add a colored left accent bar per card (6px wide):
  Reserve Mining Data -> gradient (purple to cyan)
  Create IMPACS -> gradient (green to orange)

Selected bot card:
- background: rgba(124,58,237,0.18)
- border: 1px solid rgba(124,58,237,0.55)

STEP 3 — TITLE BAR + TAB TOGGLE (SMALL, CLEAN, NOT WHITE)
- Title bar background: rgba(255,255,255,0.03)
- Border-bottom: 1px solid var(--border)
- Title text: var(--text), weight 600
- Editor/Executions segmented toggle:
  container background: rgba(255,255,255,0.06)
  border: 1px solid rgba(255,255,255,0.10)
  active tab: background rgba(255,255,255,0.10), text var(--text)
  inactive: text rgba(229,231,235,0.65)
  height: 28px, font-size: 12px
  border-radius: 10px is OK here only (it looks modern); everything else can stay square.

STEP 4 — CANVAS VISUALS (MAKE IT “N8N-LIKE” BUT POLISHED)
Canvas container:
- background: var(--surface)
- border: 1px solid var(--border)
- shadow: var(--shadow)
- remove rounded corners if currently required; otherwise allow subtle radius 10px ONLY on outer canvas (choose one; consistent).

Grid:
Use a visible but elegant grid on dark surface:
background-image:
  linear-gradient(to right, rgba(255,255,255,0.06) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(255,255,255,0.06) 1px, transparent 1px),
  linear-gradient(to right, rgba(255,255,255,0.03) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(255,255,255,0.03) 1px, transparent 1px);
background-size: 120px 120px, 120px 120px, 24px 24px, 24px 24px;

Also add a subtle vignette overlay inside canvas:
::after overlay with radial-gradient(transparent 40%, rgba(0,0,0,0.35) 100%) and pointer-events none.

STEP 5 — CANVAS NODES (MAKE THEM POP)
Node cards on canvas:
- background: rgba(255,255,255,0.08)
- border: 1px solid rgba(255,255,255,0.12)
- box-shadow: 0 10px 24px rgba(0,0,0,0.25)
- Title color: var(--text)
- Secondary labels: var(--muted)
- Add top accent strip on node matching bot type gradient (same as library).
- Hover: border rgba(6,182,212,0.55), slight lift.

Connection dots/ports:
- make them brighter (cyan) with glow:
  box-shadow: 0 0 0 3px rgba(6,182,212,0.20)

Links/edges:
- if configurable: use gradient stroke or brighter line; otherwise keep existing but increase contrast.

STEP 6 — CLEAR BUTTON (IN CANVAS, BOTTOM RIGHT, DANGER)
You already have Clear inside canvas. Make it look “tool-grade”:
- background: #ef4444
- border: 1px solid #b91c1c
- color: white
- border-radius: 0 (square)
- position: absolute; right: 16px; bottom: 16px;
- shadow: 0 8px 18px rgba(0,0,0,0.30)
- show only when canvas has >=1 node (bind to existing node-count state if available; otherwise keep always visible)

STEP 7 — GENERAL TYPOGRAPHY + SPACING
- Use one modern font stack (system font ok) and normalize:
  body font-size 13px, headings 12–14px, muted 11–12px
- Increase whitespace:
  sidebar padding 16px
  consistent 10–12px gaps

DELIVERABLE
- Unified diff only
- List files modified
- Confirm no changes to logic (only CSS/markup)


UI FIX — EDITOR / EXECUTIONS TOGGLE NOT FULLY VISIBLE (CLIPPING / OVERFLOW / Z-INDEX)

GOAL
Make the "Editor | Executions" segmented toggle fully visible at all window sizes.
Fix any clipping caused by overflow/height/padding/z-index or titlebar drag region.

STRICT RULES
- UI/CSS/layout only.
- Do NOT change any business logic or tab-switch logic.
- Do NOT change event handlers; only fix positioning and container sizing.

------------------------------------------------------------
STEP 1 — IDENTIFY THE TOGGLE CONTAINER
Locate the component/HTML that renders:
[Editor] [Executions]
(usually a segmented control / tab switcher near the top center)

Wrap it in a dedicated container:
<div class="modeToggleBar">
   ...segmented toggle...
</div>

------------------------------------------------------------
STEP 2 — PLACE TOGGLE IN A NON-CLIPPED TOP BAR
Ensure the toggle lives inside a top header area that:
- has a fixed height
- has padding
- does NOT have overflow hidden
- sits above canvas

Required header styles (apply to header/topbar wrapper):
height: 52px;
display: flex;
align-items: center;
justify-content: center;
padding: 10px 12px;
position: relative;
z-index: 50;
overflow: visible;

If there is an existing topbar, apply these styles to it.
If not, create one and move only the toggle into it (no logic change).

------------------------------------------------------------
STEP 3 — REMOVE CLIPPING FROM PARENT CONTAINERS
Search for any parent containers around the topbar/toggle that have:
overflow: hidden;
or fixed height smaller than 52px

Fix:
- Set overflow: visible on the immediate parent(s) of the toggle
- Ensure the container that hosts both topbar and canvas uses:
  min-height: 0;
  display: flex;
  flex-direction: column;

IMPORTANT: Only adjust containers affecting the top bar/toggle.

------------------------------------------------------------
STEP 4 — ELECTRON TITLEBAR / DRAG REGION (IF APPLICABLE)
If this is Electron/custom title bar:
Sometimes a draggable region hides controls.

For the top bar region:
- Keep draggable only where needed
- Ensure the toggle container is NOT draggable so it can receive clicks and render properly.

Add:
.modeToggleBar {
  -webkit-app-region: no-drag;
}

If you use a global draggable header, set:
.header { -webkit-app-region: drag; }
.modeToggleBar { -webkit-app-region: no-drag; }

------------------------------------------------------------
STEP 5 — Z-INDEX AND POSITION
Make sure the toggle is above the canvas:
.modeToggleBar { position: relative; z-index: 60; }

If canvas has overlays, ensure they are below 60.

------------------------------------------------------------
STEP 6 — RESPONSIVE FALLBACK
If the window becomes narrow, prevent the toggle from compressing into invisibility:
.modeToggleBar { min-width: 220px; }
.segmentedToggle { height: 28px; }
.segmentedToggle button { padding: 0 12px; font-size: 12px; }

------------------------------------------------------------
DELIVERABLE
Return:
1) unified diff
2) files modified
3) short explanation: which overflow/height/drag-region caused clipping and how it was fixed
4) confirm: toggle fully visible and clickable at min window size (e.g., 1024x600)


