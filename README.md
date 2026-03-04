========================
PROMPT 1 — LAYOUT STRUCTURE
========================

TASK
Refactor the current UI layout of the Workflow Creator to follow a modern workflow builder structure similar to n8n.

STRICT RULES
- DO NOT modify any business logic.
- DO NOT modify workflow execution code.
- DO NOT modify drag-and-drop behavior.
- DO NOT modify API calls.
- DO NOT modify backend logic or data models.
- Only change UI layout containers and styling.

GOAL
Reorganize the screen into three panels.

LEFT PANEL
Available Bots

CENTER PANEL
Workflow Canvas

RIGHT PANEL
Bot Details / Inspector

HEADER
Add a top header containing:

Workflow Builder
Workflow Name
Active Toggle
Save Button

Example layout:

--------------------------------------------------
Workflow Builder                 Active ○   Save
Mining → IMPACS Transaction
--------------------------------------------------

Create layout containers using a flexible grid or flex layout:

Left Sidebar width: ~260px
Right Panel width: ~320px
Center Canvas fills remaining width.

Do not move or rewrite logic code — only reorganize UI components.



========================
PROMPT 2 — AVAILABLE BOTS SIDEBAR
========================

TASK
Simplify the left panel so it only shows "Available Bots".

STRICT RULES
- Do not modify bot execution logic.
- Do not change drag-drop functionality.
- Do not change bot metadata structures.

REQUIREMENTS

Remove or hide:

Collection labels
BOT/API toggle buttons
Any collection filters

Replace with a single section:

Title: Available Bots
Subtitle (optional): Drag bots onto canvas to build workflow

Add a search field at the top.

Placeholder:
Search bots…

Search should filter the already loaded bot list client-side only.

Bot items should appear as draggable cards.

Example:

--------------------------------
Reserve Mining Data
Fetch mining account information
--------------------------------

--------------------------------
Create IMPACS Transaction
Create transaction record
--------------------------------

Card style:

background: white
border: 1px solid #D6D9DE
border-radius: 8px
padding: 12px
margin-bottom: 10px
cursor: grab

Sidebar must scroll if bot list grows.



========================
PROMPT 3 — WORKFLOW CANVAS DESIGN
========================

TASK
Improve the visual design of workflow nodes and canvas without altering functionality.

STRICT RULES
- Do not change node logic.
- Do not modify node connection code.
- Do not modify event handlers.

CANVAS

Move the existing canvas into the center panel.

Add a light grid background.

background-color: #F5F7FA

Grid lines: very subtle light gray.

NODE DESIGN

Nodes should appear as clean enterprise cards.

Example node layout:

-----------------------------------
Reserve Mining Data
BOT

Output
MiningRefId
Status
-----------------------------------

STYLE

background: white
border: 1px solid #D6D9DE
border-radius: 8px
box-shadow: 0 1px 3px rgba(0,0,0,0.1)
padding: 10px

Selected node highlight:

border-color: #2563EB

Do not change connection handles or node ports.



========================
PROMPT 4 — BOT DETAILS PANEL + EXECUTION TOOLBAR
========================

TASK
Add a right-side Bot Details panel and a bottom execution toolbar.

STRICT RULES
- Do not modify backend logic.
- Do not change workflow execution functions.
- Reuse existing button handlers.

RIGHT PANEL (Bot Inspector)

Width: ~320px

When a node is clicked show:

BOT DETAILS

Bot Name
Bot Description

Inputs
AccountId
ProductCode

Outputs
MiningRefId
Status

FIELD MAPPING

Example:

MiningRefId → MiningRefId
Status → Status

Use existing metadata only.

BOTTOM TOOLBAR

Add a horizontal toolbar at the bottom of the canvas.

Buttons:

Validate Flow
Run Workflow
View Flow JSON
Clear Canvas

Example:

-------------------------------------

[ Validate ]   [ Run Workflow ]   [ View Flow ]   [ Clear ]

-------------------------------------

STYLE

border-radius: 6px
padding: 10px 18px
primary button color: #2563EB
text color: white

Secondary buttons should be gray.

Do not introduce new backend calls.
Reuse current handlers.
