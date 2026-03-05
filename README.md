Match the Editor/Executions switch UI to the attached reference screenshot EXACTLY (n8n-style segmented control).

GOAL (pixel-close):
- A small segmented control centered in the title bar area.
- Outer container: light gray background, 1px light border, subtle rounded corners (8px), height ~26px, minimal padding.
- Two segments: “EDITOR” and “EXECUTIONS” (ALL CAPS).
- Selected segment: white background, 1px border, subtle shadow, darker text.
- Unselected segment: transparent/light gray background, muted text.
- Spacing between the two labels must be tight like the screenshot; overall control must be compact (not tall).
- Must be vertically centered within the title bar and never clipped/cropped at any window size.

IMPLEMENTATION REQUIREMENTS:
1) Find the component that currently renders the tab buttons (Editor/Executions). Replace with a single `SegmentedTabs` component that renders:
   - a wrapper container
   - two buttons inside
2) Styling must be done via the repo’s existing styling approach (CSS module / styled-components / inline styles — use whatever is already used).
3) Ensure the selected state is obvious and identical to the screenshot (white pill inside gray pill).
4) Remove any rounded corner exaggeration; keep it subtle like the screenshot.
5) Ensure clicking tabs never triggers any popup/modal/dialog/alert; it must only switch the view.

DELIVERABLES:
- Provide the updated component code + CSS.
- List exact files changed.
- After implementation, verify the switch is centered and matches the screenshot in size, border, colors, and selected/unselected look.
