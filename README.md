PROMPT — FINTECH UI POLISH v2 (GRID TONE + ALIGNMENT + TITLEBAR + SPACING) — UI ONLY

CONTEXT (CURRENT STATE)
- Grid is too thick/dark.
- “BOT LIBRARY” title and count are misaligned.
- “Drag bots onto canvas…” needs a divider line (left panel) between title area and list area.
- Too much vertical/inner spacing between title bar, left panel, and canvas.
- Window/title bar area looks plain (needs background + font color update).

STRICT RULES
- CSS/UI only. Do NOT change business logic, drag/drop logic, canvas logic, execution logic, or polling logic.
- Do NOT rename existing IDs/classes referenced by JS. You may ADD wrapper classes if necessary.
- Return: unified diff + files changed + checklist.

========================================================
1) GRID — TONE DOWN BUT CLEARLY VISIBLE
========================================================
Wherever canvas grid background is defined (CSS background-image OR library grid config):

TARGET LOOK:
- Thin, light gray lines (not blue), still visible.
- Two-layer grid: minor + major. Minor subtle, major slightly stronger.
- Ensure line thickness is 1px only.

If grid is CSS background-image, update to:

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

Notes:
- This yields gray grid (using slate/ink black at low opacity).
- If still too dark, reduce to 0.06 / 0.03.
- If too light, increase slightly to 0.10 / 0.05 (but do NOT exceed 0.10).

Also ensure the canvas surface does NOT have thick border:
- border: 1px solid #D6E4FF OR border: none;
- border-radius: 0 !important;

========================================================
2) BOT LIBRARY TITLE + COUNT ALIGNMENT
========================================================
Fix header layout:
- “BOT LIBRARY” left aligned
- Count “2” aligned on same baseline to the right of title (or as a chip)
- No odd spacing / wrapping.

Implement header as a flex row:
.botLibraryHeaderRow {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 8px;
}

If count is currently plain text, convert to a small chip:
.botCountChip {
  font-size: 11px;
  font-weight: 700;
  padding: 2px 8px;
  background: #E8F0FF;
  border: 1px solid #D6E4FF;
  color: #1D4ED8;
  border-radius: 999px;
  line-height: 1;
}

IMPORTANT:
- Do NOT change the data source of the count; only wrap/stylize.
- Ensure no extra margin pushing the count down (reset margin: 0).

========================================================
3) ADD DIVIDER LINE IN LEFT PANEL (BETWEEN HEADER AREA AND LIST AREA)
========================================================
We want a clear separator line after:
- Title + subtitle (“Drag bots onto canvas…”) + search box
and before the bot list cards.

Add:
.botLibraryDivider {
  height: 1px;
  background: #D6E4FF;
  margin: 10px 0 10px 0;   (tight)
}

Place divider in markup (preferred) right before the list container.
If markup change is risky, apply border-top to the list container:
.botListContainer { border-top: 1px solid #D6E4FF; padding-top: 10px; }

========================================================
4) REDUCE SPACE: TITLE BAR + LEFT/CANVAS SECTION
========================================================
Goal: tighter, more professional density.

A) Reduce overall top padding/margins:
- The main content wrapper below title bar should start closer to top.
Example:
.mainContainer { padding-top: 10px; }  (reduce if currently 20–30)

B) Reduce left panel internal spacing:
- header spacing tighter:
.botLibraryPanel { padding: 12px; } (reduce if larger)
- search input margin-bottom: 8px
- bot cards gap: 10px (not 16+)

C) Reduce gap between left panel and canvas:
- If using CSS grid/flex with gap, set:
.layoutGrid { gap: 12px; }  (or 10px)

D) Canvas padding:
- Keep a small inner padding only if required, else 0.
.canvasSurface { padding: 0; }

========================================================
5) TITLE BAR / WINDOW TOP AREA — ADD BACKGROUND + FONT COLOR
========================================================
We want the top header strip behind “Workflow Creator” + Editor/Executions to feel like an app header.

Apply:
- Background: linear-gradient(180deg, #0B1F3A 0%, #0A2A52 100%)  (fintech navy)
- Text: #FFFFFF or #EAF2FF for secondary
- Height: ~44px (not tall)

Example CSS:
.appTitleBar {
  background: linear-gradient(180deg, #0B1F3A 0%, #0A2A52 100%);
  color: #FFFFFF;
  height: 44px;
  display: flex;
  align-items: center;
  padding: 0 14px;
}

.appTitleBar .title {
  font-weight: 700;
  font-size: 14px;
  color: #FFFFFF;
}

appTitleBar icons/buttons (minimize/close area) must remain visible:
- If they are OS-native and can’t be styled, do NOT break them.
- If they are HTML buttons, set their icon color to #EAF2FF and hover bg to rgba(255,255,255,0.10).

Also tighten spacing between title bar and content:
- Content wrapper margin-top: 8px (not 20+)

========================================================
6) OUTPUT REQUIRED
========================================================
Return:
1) Unified diff patch
2) Files changed
3) Checklist:
  [ ] Grid is thinner + lighter gray, still visible
  [ ] BOT LIBRARY + count aligned on one row
  [ ] Divider line added between header/search and bot list
  [ ] Reduced spacing: title bar + left/canvas + gaps
  [ ] Title bar has background + readable font colors (fintech navy)

IMPLEMENTATION INSTRUCTIONS
- Locate and edit the CSS file(s) currently controlling: title bar, bot library panel, canvas background/grid.
- If needed, add minimal wrapper classes in the HTML/JSX templates ONLY for styling hooks (no logic changes).
- Avoid inline styles; prefer CSS classes.

NOW APPLY THESE CHANGES AND PROVIDE THE PATCH.
