---
name: build-a-page
description: Build a new Beaver Builder page from a description, section by section, on brand. Use when the person asks for a new page such as a home page, services page, about page or landing page.
---

# Build a page

One page at a time. One section at a time. Look at it before you call it done.

## Recipe

1. **Load the brand.**
   `get_design_tokens`
   Apply the palette, fonts, button style and corner radius to every section you build. If it
   comes back with `configured: false`, offer the set-up-my-brand skill, or carry on with the
   neutral defaults and say plainly that the result will not be on brand.

2. **Agree the outline first.**
   List the sections you intend to build, in order, in one short list. Get a yes before you
   build. This is where changes are cheap.

3. **Check for saved components.**
   `list_components`
   Check this before you build any common section: a hero, a page banner, a trust row, cards,
   pricing, a call to action, testimonials, questions and answers, a newsletter sign up, a
   video. Where a saved component matches, `place_component` is faster and stays on brand. Card
   and feature grids are the exception: build those yourself when the page wants a different
   card count or a different arrangement.

4. **Learn the shapes.**
   `get_module_schema("section")` for the section structure, then
   `get_module_schema("<slug>")` for each module type you plan to use. Do this before writing
   any section, not after a rejection.

5. **Find real images.**
   `list_media_library` to search what they already have, or `get_post_images`, which returns
   only the images the person picked for that page with the **Save selected images for MCP**
   button in the page editor. Never invent an image reference. If nothing suitable exists, use
   an obvious placeholder and tell them.

6. **Create the page.**
   `create_page` with a `title`. It is created as a draft, which is what you want. Keep the
   `page_id` and the `page_url` it returns.

7. **Add the sections, one call each.**
   `add_section` per section, in order. After each one, check the call succeeded before moving
   to the next. Do not compose the whole page into a single payload.
   If a call times out, `list_sections` first to see whether it actually landed, so you do not
   add it twice.
   For a saved component, `place_component` instead, with per page overrides for its copy and
   its image.

8. **Wire it in, if asked.**
   `set_front_page` to make it the home page. `create_menu` to build the navigation. Both
   change the whole site, so ask first.

9. **Look at it.** Run the check-a-page skill on the new page. Fix what you find, through the
   tools, then look again.

10. **Report.** Tell them the page address, that it is a draft, what you built, and anything
    you used a placeholder for.

## Notes

- If a section is rejected, read the reason, fetch the schema for that module again and fix the
  input. Never patch around a refusal.
- Do not publish unless they ask.
- The tools are the only way to change the site. Never use curl, wget, fetch or any script
  against the site.
- What each tool does is written on the tool itself, and that description arrives with the
  connection. Read it there. The summaries here are only a route map.
