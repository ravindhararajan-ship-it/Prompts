BUGFIX — AVAILABLE BOTS SCROLLBAR STILL VISIBLE

TASK
Fix the Available Bots sidebar so:
- scrolling works
- NO vertical scrollbar is visible
- NO horizontal scrollbar appears
- the sidebar does not show a bottom horizontal scroll strip

STRICT RULES
- DO NOT change business logic
- DO NOT change drag/drop behavior
- Only CSS/layout changes in the sidebar

DIAGNOSE FIRST (MANDATORY)
1) Identify the exact DOM element(s) that are scrolling in the Available Bots panel.
2) Identify which element is causing any horizontal overflow.
Output: the element class/id names and CSS overflow settings.

IMPLEMENT FIX
A) Sidebar wrapper
- overflow: hidden;
- min-width: 0;
- prevent horizontal scrolling

B) Bot list container (ONLY this should scroll)
- overflow-y: auto;
- overflow-x: hidden;
- height: 100%;
- min-height: 0; (critical for flex layouts)
- padding-right: 6px; (optional to prevent content touching edge)

C) Hide scrollbar ONLY on bot list container
- For webkit:
  .botList::-webkit-scrollbar { width: 0px; height: 0px; }
- For Firefox:
  .botList { scrollbar-width: none; }
- For old Edge/IE (if applicable):
  .botList { -ms-overflow-style: none; }

D) Ensure correct flex sizing
If sidebar uses flex column:
- parent: display:flex; flex-direction:column;
- header/search: flex: 0 0 auto;
- list: flex: 1 1 auto; min-height:0;

E) Remove default margins/padding that can create overflow
- Ensure no child cards exceed width:
  cards: max-width: 100%; box-sizing: border-box;

DELIVERABLE
- Unified diff only.
- Show exactly which element you applied the .botList class to.
- Confirm: “Only bot list scrolls; sidebar wrapper does not scroll”.
