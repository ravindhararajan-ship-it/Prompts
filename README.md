TASK
Refactor the current UI layout of the Workflow Creator to follow a modern n8n-style workflow builder design.

IMPORTANT RULES (DO NOT BREAK)

- DO NOT modify any existing business logic.
- DO NOT modify workflow execution logic.
- DO NOT modify drag-and-drop functionality.
- DO NOT modify bot execution functions.
- DO NOT modify API calls or backend logic.
- DO NOT change data models or workflow JSON generation.
- Only modify UI layout, CSS styling, and component placement.
- Reuse all existing event handlers and data bindings.

GOAL

Reorganize the screen into three main panels similar to modern workflow automation tools (n8n / Azure Logic Apps):

1. LEFT PANEL – Available Bots
2. CENTER PANEL – Workflow Canvas
3. RIGHT PANEL – Bot Details / Inspector

Also add a bottom execution toolbar.

--------------------------------------------------

NEW SCREEN STRUCTURE

TOP HEADER

Display:

Workflow Builder
Workflow Name
Active Toggle
Save Button

Example layout:

--------------------------------------------------
Workflow Builder                Active ○        Save
Mining → IMPACS Transaction
--------------------------------------------------

--------------------------------------------------

LEFT PANEL – AVAILABLE BOTS

Width: ~260px

Replace any existing "Collection", "BOT/API", or toggle filters with a single section titled:

Available Bots

Optional subtitle:
"Drag bots onto the canvas to build workflow"

Add search input at the top.

Search placeholder:
Search bots…

Search should filter the existing list client-side only.
Do not change backend logic.

Bot list items should appear as cards.

Example bot card:

--------------------------------
Reserve Mining Data
Fetch mining account information
--------------------------------

--------------------------------
Create IMPACS Transaction
Creates IMPACS transaction record
--------------------------------

Bot cards must remain draggable using the existing drag logic.

Style rules:

background: white
border-radius: 8px
border: 1px solid #D6D9DE
padding: 12px
margin-bottom: 10px
cursor: grab

Sidebar should scroll if bot list grows.

--------------------------------------------------

CENTER PANEL – WORKFLOW CANVAS

This panel must contain the existing workflow canvas.

Do NOT rewrite canvas logic.

Only move it to the center container.

Canvas layout rules:

- Occupies remaining horizontal space
- Light grid background

Grid style:

background-color: #F5F7FA
grid-lines: very light gray

Nodes remain exactly as currently implemented.

--------------------------------------------------

WORKFLOW NODE VISUAL STYLE

Improve node appearance but keep functionality identical.

Example node design:

-----------------------------------
Reserve Mining Data
BOT

Output
MiningRefId
Status
-----------------------------------

Style rules:

background: white
border: 1px solid #D6D9DE
border-radius: 8px
box-shadow: 0 1px 3px rgba(0,0,0,0.1)

Selected node highlight:

border-color: #2563EB

Do NOT change node connection handles or logic.

--------------------------------------------------

RIGHT PANEL – BOT DETAILS / INSPECTOR

Width: ~320px

This panel shows information about the selected bot.

Panel updates when user clicks a node in the canvas.

Display:

BOT DETAILS

Bot Name
Bot Description

Inputs
AccountId
ProductCode

Outputs
MiningRefId
Status

Field Mapping Section

Example mapping:

MiningRefId → MiningRefId
Status → Status

This panel must read existing bot metadata.
Do not introduce new backend logic.

--------------------------------------------------

BOTTOM EXECUTION TOOLBAR

Add a centered toolbar at the bottom of the canvas.

Buttons must reuse existing handlers.

Buttons:

Validate Flow
Run Workflow
View Flow JSON
Clear Canvas

Example layout:

--------------------------------------------------

[ Validate ]   [ Run Workflow ]   [ View Flow ]   [ Clear ]

--------------------------------------------------

Button style:

border-radius: 6px
padding: 10px 18px
background: #2563EB
color: white

Secondary buttons: gray.

--------------------------------------------------

FINTECH UI STYLE GUIDELINES

Use a clean enterprise palette.

Background: #F5F7FA
Border: #D6D9DE
Primary Blue: #2563EB
Text: #1F2937
Muted Text: #6B7280

Spacing should feel dense but clean.

--------------------------------------------------

FINAL EXPECTED LAYOUT

---------------------------------------------------------------
Workflow Builder                                 Save
---------------------------------------------------------------

Available Bots      Workflow Canvas           Bot Details
---------------------------------------------------------------

Reserve Mining Data      [Reserve Mining Data]     Inputs
Create IMPACS                 │                    AccountId
Transaction                   ▼                    ProductCode
                       [Create IMPACS Transaction]

---------------------------------------------------------------

      [ Validate ]   [ Run Workflow ]   [ View Flow ]

---------------------------------------------------------------

IMPORTANT

Do not break existing functionality.

Only restructure layout containers and styling.
All current workflows must continue to work exactly as before.
