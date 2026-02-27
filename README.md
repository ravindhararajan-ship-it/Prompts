# PromptsCompletely restyle BOT Library to match n8n-level visual strength.

This is not a minor tweak.
Override existing styles.

Do NOT change logic.
Do NOT change layout structure.
Only replace styling.

REQUIREMENTS:

1) Sidebar container
- Background: #F9FAFB
- Clear right border: 1px solid #E5E7EB
- Padding: 12px

2) Row design
- Height: 48px fixed
- Padding: 12px
- Border-radius: 10px
- No faded backgrounds
- No low opacity washout

3) Hover
- Background: #EEF2FF
- Immediate, visible feedback

4) Selected row
- Background: #E0EAFF
- Strong 4px left accent bar: #2563EB
- Slight elevation (subtle shadow)
- Must look clearly selected

5) Badge
- Size: 24px
- Radius: 8px
- Solid #2563EB background
- White bold letter
- No pastel tint
- Must feel strong and visible

6) Text
- Title: #111827, medium weight
- Description: #4B5563, 90% opacity
- Tight spacing (4px under title)
- 1-line ellipsis

7) Alignment
- 10px gap badge → text
- Perfect vertical centering
- No inconsistent margins

Goal:
Sidebar must feel structured, confident, SaaS-grade.
Not pale. Not washed. Not prototype.

Return only full style override code.
No explanation.
