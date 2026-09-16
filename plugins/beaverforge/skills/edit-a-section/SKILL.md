---
name: edit-a-section
description: Change one part of an existing page without disturbing the rest. Use for make this section darker, change that heading, swap this image, move the testimonials up, or remove that block.
---

# Edit a section

Find it, read it, change the smallest thing that does the job, then look at it.

## Recipe

1. **Find the page.**
   `list_pages`, or `get_connected_page` when they say "this page" or "the page I have open".

2. **Find the section.**
   `list_sections` for the one line summary of every section with its id. If that is not
   enough to be sure which one they mean, `get_page_layout` for the fuller picture.

3. **Read it before you change it.**
   `get_section` for the one you are about to touch. Never edit a section you have not read.

4. **Pick the smallest tool that does the job.**
   - Background colour, background image, padding, width, borders: `edit_row`. It changes only
     the settings you send and leaves every module and column exactly as they are.
   - One heading, one paragraph, one button, one image: `edit_module`. Settings you do not send
     keep their stored values.
   - Add one thing into an existing column or box: `add_module`.
   - Remove one thing: `delete_module`.
   - Move one thing: `move_module`.
   - Rebuild the section's content or structure: `edit_section`. Use this last, not first,
     because it rebuilds the row.
   - Whole sections: `delete_section`, `duplicate_section`, `reorder_sections`.

5. **Stop and ask if it is shared.** If `get_page_layout` shows the section is a placed
   component, it renders from a shared template. Correcting the copy on this page only is
   `edit_component_overrides`. Changing it is `design_component`, and that changes it on every
   page it appears on, so ask first and say so plainly. The same goes for menus, the header, the
   footer and the Style Guide.

6. **Leave the words alone.** Change only what they asked for. If they asked for a colour, do
   not improve the copy while you are in there.

7. **Look at it.** Run the check-a-page skill on the page. Confirm the change landed and that
   nothing next to it broke.

## Notes

- If an edit is refused because it would remove an image, ask the person; only on a yes pass
  `allow_image_removal: true`.
- If a call times out, read the page back before retrying, so you do not duplicate anything.
- The tools are the only way to change the site. Never use curl, wget, fetch or any script
  against the site.
- What each tool does is written on the tool itself, and that description arrives with the
  connection. Read it there. The summaries here are only a route map.
