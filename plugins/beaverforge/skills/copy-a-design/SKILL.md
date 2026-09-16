---
name: copy-a-design
description: Recreate an existing design as a real, editable Beaver Builder page from a screenshot, from pasted HTML, or from a web address. Use when the person says copy this page, rebuild this design, make my site look like this, or hands over a mock-up image.
---

# Copy a design

Every source ends up in one of three routes. Work out which one you have, follow it, then
check the result with your own eyes.

## Recipe

1. **Work out which source you have.** A screenshot image, a web address, or HTML they pasted
   or saved. A screenshot exported from a design mock-up counts as a screenshot.

2. **Ask which page it is for.** A new page, or an existing one they want rebuilt. For a new
   one, `create_page` with a title. It is created as a draft.

3. **Follow the route for that source.**

   **A screenshot.** Ask the person to upload the image into the WordPress Media Library.
   Then find it with `list_media_library` and take its address from what comes back. Call
   `recreate_from_screenshot` with that address as `image_url`. If they cannot upload it, pass
   the image itself as `image_base64` instead; that is the fallback, and only workable for a
   small image. The tool runs the picture analysis and hands back a section by section plan.
   Follow the plan in the order it gives and build each section with `add_section`.

   **A web address.** Open the address in the browser and take a full page screenshot at 1280
   wide. That screenshot is now your source: follow the screenshot route above with it. You
   may open someone else's page in the browser to look at it, but you never scrape it and
   never script it, and you never request any address directly, their own site included, with
   `curl`, `wget`, `fetch` or the WebFetch tool.

   **Pasted or saved HTML.** Read the file they hand you. Then load the plugin's copy
   instructions: they arrive with the connection as the resource
   `beaverforge://html-copy-playbook`. In Claude Code you read it by typing
   `@beaverforge:beaverforge://html-copy-playbook`, where `beaverforge` is the name your
   server has; use your own server's name if it differs. Follow those instructions and build
   the page with `add_section`.

4. **Build what the plan says.** `add_section` one section at a time, in order. Reproduce the
   source's own colours, fonts and spacing. A copy is meant to match the source, so do not
   apply the site Style Guide over the top unless they ask for it.

5. **Self check as you go.** After each section, `get_section` to confirm what landed, and
   `edit_module` to correct anything off before you move to the next one.

6. **Look at it.** Run the check-a-page skill. Then compare it against the source side by side,
   at desktop and at phone width, and fix the differences that matter: wrong colours, wrong
   spacing, missing images, text that does not match.

7. **Report.** Say what matched, what did not, and what you had to approximate.

## Notes

- Never request the source page, or their own site, with `curl`, `wget`, `fetch`, the WebFetch
  tool or a script. A browser is the only thing you use to look at a page.
- Only copy a design the person has the right to copy. If it looks like someone else's live
  site, say so and ask.
- Copy the design, not the claims. Do not carry over another company's name, testimonials,
  prices or statements of fact into their page unless they tell you to.
- What each tool does is written on the tool itself, and that description arrives with the
  connection. Read it there. The summaries here are only a route map.
