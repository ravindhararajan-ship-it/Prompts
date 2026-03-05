UI REFACTOR — MOVE EDITOR / EXECUTIONS TO TITLE BAR CENTER

GOAL
Move the Editor / Executions toggle into the title bar area and center it horizontally, similar to modern workflow tools.

STRICT RULES
- Do NOT change tab switching logic.
- Do NOT modify execution logic.
- Layout + CSS only.

STEP 1 — RESTRUCTURE TITLE BAR

Locate the title bar container where "Workflow Creator" and window controls are rendered.

Convert it into a 3-zone layout:

TitleBar
  LeftSection      → Workflow Creator title
  CenterSection    → Editor / Executions toggle
  RightSection     → window controls + run status

CSS:

TitleBar
display: flex;
align-items: center;
justify-content: space-between;
padding: 8px 16px;
height: 40px;

LeftSection
flex: 1;
display: flex;
align-items: center;

CenterSection
flex: 0;
display: flex;
justify-content: center;
align-items: center;

RightSection
flex: 1;
display: flex;
justify-content: flex-end;
align-items: center;
gap: 10px;

STEP 2 — MOVE TOGGLE

Move the existing Editor / Executions segmented control into CenterSection.

Do not change any event handlers.

STEP 3 — COMPACT N8N STYLE

SegmentContainer
display: inline-flex;
background: #EEF2F6;
border: 1px solid #D0D5DD;
border-radius: 0;
overflow: hidden;
height: 28px;

SegmentButton
padding: 4px 12px;
font-size: 12px;
border: none;
background: transparent;
border-right: 1px solid #D0D5DD;
cursor: pointer;

SegmentButton:last-child
border-right: none;

ActiveSegment
background: #FFFFFF;
font-weight: 600;

STEP 4 — AVOID WINDOW CONTROL COLLISION

Ensure the toggle never overlaps the system window buttons:

CenterSection
position: absolute;
left: 50%;
transform: translateX(-50%);

STEP 5 — VERIFY

Confirm:
- Editor / Executions sits centered in title bar
- Title remains left aligned
- Window controls stay right aligned
- Header height remains compact

DELIVERABLE
- Unified diff only
- List files modified


UI REDESIGN — CONVERT "AVAILABLE BOTS" PANEL INTO ENTERPRISE BOT LIBRARY

GOAL
Redesign the left sidebar "Available Bots" section to an enterprise-style Bot Library panel with card-based bots, search bar, and improved visual hierarchy.

STRICT RULES
- DO NOT modify any workflow logic.
- DO NOT modify drag/drop implementation.
- DO NOT modify bot execution logic.
- Only change UI layout and styling of the sidebar.

---------------------------------------------------

STEP 1 — RENAME PANEL HEADER

Change the sidebar header text from:

"Available Bots"

to

"BOT LIBRARY"

Header style:

font-size: 13px
font-weight: 600
letter-spacing: 0.04em
color: #374151
padding-bottom: 8px
border-bottom: 1px solid #E5E7EB

---------------------------------------------------

STEP 2 — ADD BOT COUNT

Display number of bots in header.

Example:

BOT LIBRARY (2)

---------------------------------------------------

STEP 3 — ADD SEARCH BAR

Add a search input below the header.

Search field design:

height: 32px
padding: 6px 10px
font-size: 13px
border: 1px solid #D1D5DB
background: #FFFFFF
border-radius: 0
outline: none
width: 100%

Placeholder text:

"Search bots..."

Focus state:

border-color: #3B82F6

---------------------------------------------------

STEP 4 — CONVERT BOT ITEMS INTO CARDS

Replace current bot list with card layout.

Each bot should appear as a rectangular card.

Card structure:

BotCard
  BotTitle
  BotDescription
  BotFooter

Example content:

Reserve Mining Data
Fetch reserve mining account details

BOT
Drag to canvas →

---------------------------------------------------

STEP 5 — CARD STYLING

Card style:

background: #FFFFFF
border: 1px solid #E5E7EB
padding: 12px
margin-bottom: 10px
border-radius: 0

Add subtle elevation:

box-shadow: 0 1px 2px rgba(0,0,0,0.05)

---------------------------------------------------

STEP 6 — BOT TITLE STYLE

BotTitle

font-size: 14px
font-weight: 600
color: #111827
margin-bottom: 4px

---------------------------------------------------

STEP 7 — BOT DESCRIPTION STYLE

BotDescription

font-size: 12px
color: #6B7280
margin-bottom: 6px

---------------------------------------------------

STEP 8 — BOT FOOTER

Footer should contain:

BOT label
Drag hint

Example layout:

BOT        Drag to canvas →

Footer style:

display: flex
justify-content: space-between
font-size: 11px
color: #9CA3AF

---------------------------------------------------

STEP 9 — ADD BOT ICONS

Add simple icons before bot titles.

Examples:

🧠 Reserve Mining Data
⚙ Create IMPACS Transaction

Icons should be inline with the title.

---------------------------------------------------

STEP 10 — ADD HOVER EFFECT

When hovering over bot card:

background: #F5F8FF
border-color: #3B82F6
cursor: grab

---------------------------------------------------

STEP 11 — SIDEBAR BACKGROUND

Set sidebar background:

background: #F8FAFC
border-right: 1px solid #E5E7EB
padding: 16px

---------------------------------------------------

STEP 12 — SIDEBAR WIDTH

Set fixed width:

width: 260px

Ensure the canvas takes the remaining screen width.

---------------------------------------------------

STEP 13 — SCROLL SUPPORT

Enable vertical scroll if bots exceed screen height.

overflow-y: auto
height: 100%

---------------------------------------------------

STEP 14 — DO NOT TOUCH

The following must remain unchanged:

- drag/drop functionality
- bot data structure
- bot execution logic
- canvas node rendering

Only the sidebar UI must change.

---------------------------------------------------

DELIVERABLE

Return:

1) unified diff
2) files modified
3) confirmation that bot drag behavior remains unchanged


