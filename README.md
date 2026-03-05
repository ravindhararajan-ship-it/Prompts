Fix the header layout so the "Editor | Executions" segmented control behaves like a compact toolbar element:

1. Reduce the control height to ~26px–28px so it appears compact.
2. Place the control fully inside the title bar container.
3. Vertically center it using flexbox (display:flex; align-items:center; justify-content:center).
4. Ensure equal top and bottom padding so it appears visually centered within the title bar.
5. Prevent overflow or clipping so the control is always fully visible.
6. Implement a clear active state:
   - Selected tab → solid background + bold text + subtle border.
   - Unselected tab → light background + muted text.
7. Keep corners square (no rounded edges) and maintain consistent spacing between tabs.

Do not change any application logic — adjust layout and styling only.



You are working inside my repo. Goal: FIX ONLY UI/UX + layout issues in Workflow Creator (Editor + Executions) and KEEP ALL EXISTING BUSINESS LOGIC / DATA FLOW / EVENT HANDLERS intact (no behavior changes except pure UI rendering + non-breaking polling for console). Do NOT remove features unless explicitly asked below. Make minimal, safe, incremental edits with clear diffs.

SCOPE (apply to BOTH Editor and Executions views where relevant):
1) HEADER / TITLE BAR
- Reduce vertical whitespace in the top area (title+tabs must not waste space).
- Add a subtle fintech-style header background (light gradient or solid light ink-blue/gray) and update font colors for contrast.
- Move the "Editor | Executions" segmented control into the title bar center, fully visible at all window sizes.
- Segmented control: smaller (match n8n-like compact tabs), no rounded corners, clear active state (active tab filled, inactive outlined), consistent height and padding, always centered.
- Remove any extra popups/overlays caused by switching tabs (no floating “Validate” popup etc.). Ensure tab switch only swaps content.

2) CANVAS (EDITOR + EXECUTIONS)
- Canvas must have NO rounded corners and NO thick/dark border. Use a 1px subtle border (light gray/ink-blue) or no border with a shadow only.
- Canvas grid must be clearly visible but subtle: thin lines, low-contrast gray (not dark), with slightly stronger major lines every N cells.
- Ensure canvas boundary is visually clear vs page background.
- Fix connector geometry: smooth curves, consistent stroke width, no awkward angles.
- Fix connector label bubble placement: centered on the connector path, not offset; does not overlap nodes/ports.
- Fix ports alignment: input/output dots centered vertically on node edges and aligned consistently across nodes.

3) NODES
- Fix node header top accent line so it NEVER overflows card width.
- Normalize node selection style: reduce glow/outline thickness to match design system.
- Fix header icon layout: menu + success/check + any status icons must not overlap; align right with spacing; never crowd title.
- Improve content hierarchy: title > type (BOT) > IO labels; reduce visual competition; consistent spacing.

4) EXECUTIONS TAB LAYOUT
- Keep the canvas visible in Executions tab (same canvas area as Editor).
- Console should look like Windows console: dark background, monospace, small font, good line height, subtle border; but MUST NOT dominate page.
- Reduce console height to ~25–30% of window by default; user can resize if splitter exists (keep if already present).
- Console header row: “Console” + status (“Running”) left-aligned as a group; controls (Steps only, Copy, Clear) right-aligned in the SAME header row and vertically centered.
- Fix the floating “Running: Step x/y …” badge: attach it to the canvas top-right INSIDE canvas with consistent padding, or move into console header (pick the cleaner option) but do not float randomly.
- Implement non-breaking async console updates: poll for new log lines every 3 seconds while execution is running, append incrementally (no full refresh), auto-scroll only if user is already at bottom; if user scrolls up, don’t yank them down.
  - Must be robust: stop polling on execution complete/cancel, and on tab switch/unmount to avoid memory leaks.
  - Do NOT change execution logic—only how logs are fetched/displayed. If there is already an endpoint/file/tail function, reuse it.

5) LEFT BOT LIBRARY PANEL (EDITOR)
- Make the left panel visually distinct from canvas (subtle tinted background).
- Fix alignment: “BOT LIBRARY” title and count must align baseline and spacing; no stray dots/bullets before items (remove DOT).
- Add a clear divider line between the “Drag bots…” helper text and the bot list area.
- Reduce wasted padding; keep compact spacing.
- Ensure icons appear for each bot (if icon assets exist, wire them; if not, add safe fallback SVG/icon component).
- Ensure the bot list scroll works reliably: vertical scroll visible when overflow; no missing scrollbar; list height properly constrained; do not scroll the entire page.

6) GENERAL POLISH
- Ensure all controls never overlap on smaller widths; use responsive layout (flex/grid) with min-widths and wrapping rules.
- No rounded corners where specified (tabs, canvas, critical buttons). Keep consistent corners elsewhere (small radius ok only if already global—but tabs/canvas must be squared).
- Do not introduce new heavy dependencies. Prefer CSS and existing components.
- After changes: run the app (or unit smoke check) and ensure no runtime errors.

DELIVERABLE
- Make the changes directly in the relevant UI files (components + CSS). Show me:
  a) Which files you changed
  b) A concise summary of what changed per file
  c) Any new constants/styles added
  d) How the 3-second console polling is implemented and cleaned up

IMPORTANT CONSTRAINTS
- DO NOT touch business logic, workflow execution order, bot execution, or data contracts.
- UI-only refactor is allowed (rearranging components, CSS, layout wrappers).

------------------
Fix the execution logging so logs from every bot step (including the second bot) appear in the UI console panel in real time.

Requirements:
1. Capture stdout and stderr from the automation process (e.g., chromedriver / python / node / cmd execution).
2. Stream those logs to the application console panel while the workflow is running.
3. Ensure logs from ALL workflow steps are appended, not replaced.
4. Use non-blocking streaming (process.stdout.on('data') or equivalent) so logs appear live.
5. Preserve log order exactly as produced by the process.
6. When switching steps (Bot1 → Bot2), continue appending logs to the same console session.
7. Do not spawn separate consoles that hide logs from the UI.
8. If the automation launches a subprocess, pipe its stdout back to the parent process and then to the UI console.
9. Ensure the UI console auto-scrolls while new logs arrive.
10. Do not modify the workflow execution logic—only fix the logging pipeline.

Goal:
The UI console should display the same log output that currently appears in cmd.exe, including logs from the second bot execution.
- If you must move a component, preserve props and behavior; no regressions.

Now implement all fixes above.
