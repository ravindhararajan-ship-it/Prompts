You are working inside THIS repo (do not create a new project). Fix ONLY the UI/logic related to: (1) Editor/Executions tabs styling + behavior, (2) remove the unwanted popup on tab click, (3) make Clear button always visible after first node is added, (4) disable Run until workflow is valid (all required connectors satisfied / nodes show green).

DO THIS STEP-BY-STEP:

A) EDITOR / EXECUTIONS TABS (n8n/GitHub segmented control)
1) Locate the component that renders the “Editor” and “Executions” switch (top title bar). Replace the current buttons with a segmented control:
   - Text must be ALL CAPS: “EDITOR” and “EXECUTIONS”
   - Container: light gray background, 1px border, subtle radius (<=8px), small height (~26–30px), centered vertically within the title bar
   - Selected tab: white background, 1px border, subtle shadow, darker text
   - Unselected tab: transparent, muted text
2) Ensure selected/unselected states are visually distinct and do not overflow/crop on any window size.

B) REMOVE POPUP ON CLICKING EDITOR
1) When switching between tabs, DO NOT open any modal/popup/window (the small OS-looking popup in screenshot must never appear).
2) Search the codebase for any usage of:
   - window.open, showModal, dialog, MessageBox, alert, confirm, prompt
   - any “Validate” dialog or any “popup” triggered by tab click
3) Remove that behavior entirely. Tab click must only switch views (Editor <-> Executions) with no dialogs.

C) CLEAR BUTTON VISIBILITY (EDITOR CANVAS)
1) Clear button must be a solid red rectangular button (no rounded corners), placed INSIDE the canvas at bottom-right with a small margin (e.g., 16px).
2) Clear must be hidden when canvas is empty.
3) As soon as at least 1 bot/node is added to the canvas, Clear must become visible and stay visible even after dragging/zoom/pan.
4) Ensure z-index so it never goes behind the canvas and never gets clipped.

D) RUN BUTTON ENABLEMENT (EXECUTIONS TAB)
1) Run button must be disabled by default.
2) Enable Run ONLY when the workflow is valid:
   - At least 1 node exists
   - All required input/output connections are satisfied (no dangling required connectors)
   - If your UI uses “green” to indicate valid nodes/connectors: Run enables ONLY when all nodes are in valid/green state and there are no validation errors.
3) Implement a single source of truth boolean like `isWorkflowValid` derived from the graph state.
4) Wire the Run button disabled/enabled state to `isWorkflowValid`.
5) Add a tooltip or small helper text when disabled: “Complete connections to enable RUN”.

E) IMPORTANT CONSTRAINTS
- Do not change business logic of bots/execution engine; only UI + validation gating.
- Do not introduce new external dependencies unless already present.
- Keep styling consistent with the current fintech theme (light UI, ink-blue accents).
- After changes, run the app and verify:
   1) Clicking EDITOR/EXECUTIONS never opens any popup
   2) Tabs show as GitHub/n8n segmented control with ALL CAPS labels
   3) CLEAR appears bottom-right after adding a bot, disappears when canvas is empty
   4) RUN disabled until workflow valid, then enables correctly

Finally: list exactly which files you modified and summarize each change in 1–2 lines.
