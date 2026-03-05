PROMPT — FINTECH UI POLISH (BOT LIBRARY + CANVAS) — NO LOGIC CHANGES

CONTEXT
We already reverted to a light fintech theme. Now refine:
1) BOT Library left section must look like “Improved Enterprise Version” (polished, with icons, no leading dots).
2) Canvas must NOT have rounded corners and must NOT have black border.
3) Canvas grid must be clearly visible using a light ink-blue.
4) Left panel must have a tinted background / header to visually differentiate from canvas.

STRICT RULES
- UI/CSS only. Do NOT modify business logic, drag/drop logic, execution logic, data polling, or component structure beyond adding wrappers/classes.
- Do NOT change any existing identifiers used by logic; only add classes if needed.
- Provide unified diff, files changed, and a short checklist of what was updated.

========================================================
A) BOT LIBRARY — ENTERPRISE LOOK + ICONS + NO DOTS
========================================================

A1) REMOVE LEADING DOTS
In the bot list rendering (JS/TS/HTML template), remove any prefix like:
"• " or "." or bullet decorators.
If dots are coming from CSS list-style, disable it:
- Ensure the container is NOT a <ul> with bullets, OR set:
  list-style: none;
  padding-left: 0;

A2) ADD ICONS FOR EACH BOT (NO EXTERNAL ASSETS REQUIRED)
We have only 2 bots:
- “Reserve Mining Data” => use a database/search style icon
- “Create IMPACS Transaction” => use a document/plus or gear icon

Implement icons using inline SVG (preferred) OR emoji as last resort.
Do NOT introduce new dependencies.
Place the icon at the left of the bot name inside the card header.

Example inline SVG approach:
- Create a small <span class="botIcon"> containing SVG
- Size 16x16, monochrome in primary blue.

A3) BOT LIBRARY PANEL DIFFERENTIATION
Apply a subtle tinted background to the left panel:
- Panel background: #F3F7FF (very light blue tint)
- Panel border-right: 1px solid #D6E4FF
- Panel header background: #E8F0FF
- Header text: #0F2B5B (deep fintech navy)

Add a “section label” chip next to “BOT LIBRARY (2)”:
- background: #DDEBFF
- text: #1D4ED8
- border-radius: 6px
- font-size: 11px
- padding: 2px 8px

A4) BOT CARDS — POLISHED ENTERPRISE
Card base:
- background: #FFFFFF
- border: 1px solid #D6E4FF
- box-shadow: 0 2px 10px rgba(15, 43, 91, 0.08)
- border-radius: 10px (allowed for cards)
- padding: 10px 10px
Hover:
- border-color: rgba(29, 78, 216, 0.45)
- box-shadow: 0 10px 22px rgba(15, 43, 91, 0.14)
Selected/Active:
- left accent bar: 4px solid #1D4ED8
- background: #F7FAFF

Typography:
- Bot name: 13px, weight 700, color #0F172A
- Description: 11px, color #475569
- “Drag to canvas →” text: 11px, color #1D4ED8 (link style)

Remove any “BOT” label that looks like a bullet row.
If we must keep BOT label, render it as a pill:
- background: #EEF5FF
- color: #1D4ED8
- border: 1px solid #D6E4FF
- padding: 2px 6px
- font-size: 10px
- border-radius: 999px

A5) SEARCH INPUT — FINTECH
- background #FFFFFF
- border 1px solid #BFD3FF
- focus ring: 0 0 0 3px rgba(29, 78, 216, 0.18)
- height: 34px
- border-radius: 10px
Add a magnifier icon inside input (CSS background-image OR inline icon in wrapper).

========================================================
B) CANVAS — SQUARE CORNERS, NO BLACK BORDER, CLEAR GRID
========================================================

B1) REMOVE ROUNDED CORNERS + BLACK BORDER
Canvas container must be square:
- border-radius: 0 !important;
Remove black border entirely:
- border: 1px solid #D6E4FF;  (light border) OR border: none;
NO thick border, NO black stroke.

B2) CANVAS GRID — LIGHT INK BLUE, CLEARLY VISIBLE
Use a 2-layer grid (minor + major). Ink-blue, subtle but clearly visible:

background-color: #FFFFFF;
background-image:
  linear-gradient(to right, rgba(29,78,216,0.10) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(29,78,216,0.10) 1px, transparent 1px),
  linear-gradient(to right, rgba(29,78,216,0.05) 1px, transparent 1px),
  linear-gradient(to bottom, rgba(29,78,216,0.05) 1px, transparent 1px);
background-size:
  120px 120px,
  120px 120px,
  24px 24px,
  24px 24px;

If grid is implemented in a <canvas> or library setting, update its grid color config accordingly (but do not change logic).

B3) CANVAS SURFACE SHADOW (SUBTLE)
- box-shadow: 0 6px 18px rgba(15, 43, 91, 0.10);
- Keep padding/margins as-is.

========================================================
C) TITLE BAR / TOGGLE (ONLY IF NEEDED)
========================================================
If Editor/Executions toggle is currently faint or blends in:
- Add a subtle container background: #F3F7FF
- Border: 1px solid #D6E4FF
- Height: 28px, font-size 12px
- Active tab background: #FFFFFF, text: #0F172A

Do NOT move toggle location in this prompt.

========================================================
D) IMPLEMENTATION DETAILS
========================================================
1) Find CSS files controlling:
- Bot library panel (left)
- Bot cards
- Canvas wrapper / canvas element

2) Add/adjust classes if necessary:
- .botLibraryPanel
- .botLibraryHeader
- .botCard
- .botIcon
- .canvasSurface

3) Ensure there are no global overrides like:
- border: 4px solid #000
- border-radius on all panels

========================================================
E) OUTPUT REQUIRED
========================================================
Return:
- Unified diff (patch)
- List of files modified
- Checklist confirming:
  [ ] No dots/bullets
  [ ] Icons visible for each bot
  [ ] Left panel has tinted background and header differentiation
  [ ] Canvas square corners
  [ ] No black border
  [ ] Grid clearly visible in light ink-blue
