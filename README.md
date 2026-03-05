PROMPT 1/4 — STABILIZE UI + REMOVE PLACEHOLDERS (NO BUSINESS LOGIC CHANGES)

ROLE: You are a senior UI engineer. You MUST only change UI/layout/styles. Do NOT change workflow execution logic, bot logic, backend calls, JSON schema, or file formats. If you need data, reuse existing state/props exactly.

GOAL:
Fix the current “unfinished” look:
- Remove the two large empty rectangles in the title bar (broken placeholders).
- Reduce title/header height to reclaim canvas space.
- Make Editor/Executions tabs visually anchored to the header, with clear active/inactive styling.
- Add a subtle separator line between header and content.

DO THIS:
1) FIND the top-level window layout component(s):
   - search for: "Workflow Creator", "Editor", "Executions", "titlebar", "header", "topbar", "toolbar", "tabs"
   - identify where the two empty rectangles are created (likely placeholder divs/panels).
   - REMOVE those placeholder containers entirely (not hidden—deleted) OR replace with real minimal header content (title left, tabs center/right).

2) Implement a single, clean header structure:
   - Left: app title “Workflow Creator”
   - Center: tabs (Editor, Executions)
   - Right: window controls remain as-is (do not break native window buttons)
   - Header height target: 44–52px (compact)

3) Tabs rules:
   - Tabs must NOT float in content space.
   - They must sit inside the header on the same row.
   - Active tab: solid background, high contrast label
   - Inactive: transparent/low-contrast
   - No rounded corners (square/enterprise look)

4) Add a subtle divider below header:
   - 1px line, light gray (or themed color if theme exists)
   - full width

OUTPUT:
- List the exact files you modified (paths).
- Provide the exact code changes (diff-style or full updated components).
- Confirm explicitly: “No business logic changed.”



PROMPT 2/4 — BOT LIBRARY PANEL POLISH + ALIGNMENT + DIVIDERS

ROLE: UI/UX + front-end engineer. UI-only changes. Do NOT modify backend/execution.

GOAL:
Make left “BOT LIBRARY” look like a real tool panel:
- Align “BOT LIBRARY” title and count “2” on the same baseline (count as a badge).
- Add a divider line between the title row and the instruction text.
- Add a subtle background to the sidebar so it’s distinct from the canvas.
- Fix card spacing and alignment, including “Drag to canvas →” positioning.
- Ensure icons are visible (no missing icons). If icons are SVG/font-based, fix CSS color/size so they render.

DO THIS:
1) Sidebar container:
   - Apply a slightly tinted background (fintech friendly): very light blue-gray.
   - Add right-side divider (1px) to separate from canvas.
   - Reduce excessive padding/empty space.

2) Title row:
   - Structure as a flex row: [BOT LIBRARY] [badge count]
   - Badge style: small pill or square badge, subtle fill, readable contrast
   - Remove any stray dot/bullet near the title (user asked “Remove DOT.”)

3) Instruction text:
   - Place directly under title row
   - Add divider line above or below it (thin 1px)
   - Reduce font size slightly; keep it readable

4) Bot cards:
   - Standardize card height, padding, and spacing
   - Make truncation consistent (ellipsis)
   - Left accent bar consistent color
   - “BOT” label and “Drag to canvas →” aligned on one row at the bottom of card
   - Ensure hover/focus styles look polished (slight elevation or border highlight)

5) Scroll behavior:
   - Bot list area must scroll properly if more bots appear.
   - Always-visible scrollbar preferred (or at least shows on hover). Ensure it’s not broken by overflow hidden on parent containers.

OUTPUT:
- Files changed + diffs.
- Confirm “No business logic changed.”



PROMPT 3/4 — CANVAS: GRID VISIBILITY + CLEAN BORDERS + NO ROUNDED CORNERS

ROLE: Front-end UI engineer. UI only.

GOAL:
Fix canvas “plain / unfinished” issues:
- Canvas must NOT have rounded corners.
- Remove any thick/black border.
- Add a clearly visible but subtle grid (not too dark/thick). User wants lighter ink-blue or gray.
- Add a subtle boundary between sidebar and canvas (divider/shadow).
- Ensure canvas fills available space (no huge wasted margins).

DO THIS:
1) Canvas container:
   - Set square corners (border-radius: 0)
   - Border: 1px subtle (light gray) OR none if grid edge is enough
   - Background: near-white with grid overlay

2) Grid implementation:
   - Use CSS background with repeating-linear-gradient (or existing grid if present)
   - Grid lines: thin (1px), low opacity
   - Prefer gray-blue tone: e.g. rgba(60, 120, 180, 0.12) OR neutral gray rgba(0,0,0,0.06)
   - Provide two layers: minor grid (small squares) and major grid (every N squares) slightly stronger but still subtle
   - IMPORTANT: Fix the prior bug where grid became too dark/thick.

3) Layout sizing:
   - Reduce header + outer paddings so canvas is larger.
   - Canvas should be flush with content area (small consistent padding only).

4) Fix node rendering glitch:
   - The node’s thick top line must NOT extend past node width.
   - Locate CSS causing a pseudo-element/underline overflow and constrain it (overflow hidden or correct width calc).

OUTPUT:
- Files changed + diffs.
- Confirm “No business logic changed.”



PROMPT 4/4 — FINAL POLISH: HIERARCHY, CONSISTENT SPACING, & VISUAL BUG FIXES

ROLE: UI polish pass. UI only.

GOAL:
Finish as “standard tool / polished product”:
- Improve overall hierarchy (header/sidebar/canvas contrast).
- Ensure consistent spacing across panels and inside cards.
- Fix any floating dots/ports that look disconnected.
- Make active states clear (selected bot card, selected node).
- Ensure Editor/Executions are fully visible (no clipping). Tabs must never be cut off at top.

DO THIS:
1) Global spacing system:
   - Define consistent spacing tokens (8/12/16)
   - Apply to header, sidebar, cards, canvas margins

2) Contrast + typography:
   - Header background: subtle tinted band (light fintech blue-gray)
   - Text colors: stronger for titles, medium for secondary text
   - Make sure labels are readable on the background

3) Ports/dots alignment:
   - Ensure input/output ports are anchored to node edges
   - Remove any “floating dot” artifacts by fixing absolute positioning or transform math
   - Do not change connection logic; only CSS/positioning

4) Selected states:
   - Selected bot card: clear highlight (border + subtle background)
   - Selected node: highlight outline/shadow (no neon)

5) Tab visibility/clipping:
   - Ensure header has enough padding and z-index
   - Tabs must be centered and fully visible across window sizes
   - Fix any overflow hidden that clips them

OUTPUT:
- Files changed + diffs.
- Confirm “No business logic changed.”
