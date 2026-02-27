The sidebar styling is NOT taking effect. Fix this by forcing a ROOT-LEVEL style override and applying it to the exact sidebar widgets.

Do NOT change logic.
Do NOT change layout structure.
Only enforce styling + ensure it applies.

MANDATORY:
1) Identify the exact widget class used for BOT rows (Listbox / Treeview / Frame rows / QListWidget / QTreeView).
2) Apply styles to THAT widget and its item delegates (not a parent container only).
3) Apply the stylesheet/theme at the ROOT application level (App/Window) so children inherit it.
4) Remove ALL opacity/alpha usage. Use solid colors only. No “light tint”, no transparency.

STYLE TARGET (must be visible):
- Sidebar bg: #F9FAFB
- Selected row bg: #E0EAFF (solid)
- Hover bg: #EEF2FF (solid)
- Left selection bar: 4px solid #2563EB (must be clearly visible)
- Badge: 24px, radius 8px, bg #2563EB (solid), text white bold

ENFORCE:
- Fixed row height: 48px
- Padding: 12px
- Badge→text gap: 10px
- Title: #111827, font-weight 600
- Desc: #4B5563, 1-line ellipsis

VERIFICATION (required in code):
- Add a temporary debug log/print confirming the style is applied (e.g., stylesheet length > 0 or style object assigned).
- If the widget is QTreeView/QListView, implement a custom delegate to paint:
  - hover background
  - selected background
  - left accent bar
  - badge rectangle + letter
  (Do NOT rely on default item rendering)

OUTPUT:
Return ONLY the final code changes that:
- apply root-level styling
- correctly style the sidebar items
- visibly change hover/selected states
No explanation.
