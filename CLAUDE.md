# Working on this website with BeaverForge AI

The person you are working with owns a WordPress site built with Beaver Builder. The
BeaverForge AI plugin on that site publishes a set of tools to you. Those tools are how you
read and change the site.

What the tools give you: the brand, whole pages, single sections, single modules, saved
components, menus, the site header and footer, WooCommerce setup, and recreating a design
from a screenshot, from HTML, or from a web address, which you open in the browser and
screenshot first. You do not need to know how any of it works inside. You describe what you
want in the shape the tools ask for, and the plugin builds it.

## Order of operations

1. **Load the brand first.** Call `get_design_tokens` before you build or edit anything, and
   apply what it returns to every section. If it comes back with `configured: false`, there is
   no brand yet: offer to set one up (see the set-up-my-brand skill) or say clearly that the
   result will not be on brand.
2. **Learn the shape before you write it.** Call `get_module_schema("section")` for the
   section structure, and `get_module_schema("<slug>")` for each module you are about to use.
3. **Build or edit.** One page at a time, one section at a time.
4. **Look at the result in a browser.** Open the page, at desktop and phone width, and judge
   it with your own eyes before you tell anyone it is done.

## Rules of engagement

- **The tools are the only way in.** Never use `curl`, `wget`, `fetch`, the WebFetch tool, a
  script, or any other direct HTTP request against the site, for reading or for writing. A
  browser is the only way to look at it. If a tool cannot do what you want, say so and stop;
  do not go around it.
- **One page or one task at a time.** Finish it, check it, then move on. Do not start three
  pages at once.
- **Ask before anything shared.** Saved components, menus, the header, the footer and the
  Style Guide affect the whole site. Say what you are about to change and wait for a yes.
- **Do not rewrite copy you were not asked to change.** If you are fixing a colour, fix the
  colour. Existing words stay exactly as they are unless the person asks for new words.
- **When the plugin refuses, read the reason and pass it on.** A refusal is deliberate and it
  says why. Tell the person the reason in plain words and ask how they want to proceed. Never
  try to work around a refusal.
- **Never invent an image.** Find real ones with `list_media_library`, or with
  `get_post_images`, which returns only the images the person picked for that page with the
  **Save selected images for MCP** button in the page editor. If there is no suitable image,
  use a clearly temporary placeholder and say you did.
- **New pages start as drafts.** `create_page` makes a draft. Leave it as a draft unless the
  person asks you to publish.

## Verification

You have not finished until you have looked. For every page you build or change:

1. Open the page URL in a browser at 1280 wide and again at 375 wide.
2. Look at it. Check the text is readable against its background, nothing overlaps, nothing
   overflows sideways, images are actually showing, buttons look like buttons, and the spacing
   between sections is even.
3. Say what you saw. If something is wrong, fix it through the tools and look again.

A draft page is not public: only a browser that is logged in to WordPress can see it. So one
of three things has to happen, and the person chooses which. They log in to WordPress
themselves in the browser window you open, and you carry on in that window. Or they open the
preview themselves and send you a screenshot. Or they ask you to publish the page. You never
type their password and you never go to the login page on their behalf.

If they are editing the page in Beaver Builder right now, `get_connected_page` tells you so,
and your edits appear on their canvas within seconds rather than on the public address.

"The tool returned success" is not verification. Reading the layout back is not verification
either. Seeing it is.

## Setting up the connection

Talk the person through this one step at a time and wait after each step.

**1. Switch the server on.**
In WordPress admin: open the **BeaverForge AI** menu, and on the page headed **BeaverForge AI
Settings** find the **MCP Server** section, then tick **Enable MCP endpoint**. Ask them to
copy the **Endpoint URL** shown just below it. It looks like
`https://their-site.com/wp-json/beaverforge-ai/v1/mcp`. If there is no **MCP Server** section
on that page, the licence is not active yet.

**2. Create a key.**
On the same screen, under **Your key**: type a **Label** (for example "Claude Code, work
laptop"), leave **Expiry** blank unless they want one, press **Create key**. The key is shown
once, so tell them to copy it now. It starts with `bfai_`.

**3. Fill in the connection file.**
Copy `.mcp.json.example` to `.mcp.json` in this folder. Ask them to paste their endpoint URL
and their key into it themselves, in their editor. **Never ask them to paste the key into the
chat, and never type a real key into a file yourself.** `.mcp.json` is ignored by git, so the
key stays on their machine.

**4. Restart.**
Claude Code reads the connection at startup. Fully quit and reopen it. A reload is not enough.
On the first launch after that it asks them to approve this project's `.mcp.json`, so tell
them to expect the prompt and say yes.

**5. Confirm.**
In the new session, call `list_pages`. A list of their pages means the connection works. If
the tools are not there at all, the restart did not happen, the approval prompt was declined,
or the file has a typo.

**If it hangs:** almost always an out of date Node. Ask them to run `node -v`. Below 20.18.1
needs an update, then a full restart of Claude Code.

### Claude Desktop

Same endpoint, same key, same command. The settings live in the desktop app's own config file
instead of `.mcp.json`. The reliable way in is the app itself: **Settings > Developer > Edit
Config**. The file is `claude_desktop_config.json`, normally at
`~/Library/Application Support/Claude/claude_desktop_config.json` on a Mac and
`%APPDATA%\Claude\claude_desktop_config.json` on Windows. Paste the same block that is in
`.mcp.json.example`, then fully quit and reopen the app.

## Handy starting points

- `list_pages` to see what exists, `list_unbuilt_pages` for older pages not yet built with
  Beaver Builder, which you then adopt with `enable_builder` before any layout tool will work
  on them, `list_posts` for blog posts and other content types.
- `get_connected_page` when they say "this page" or "the page I have open".
- `list_components` before building a common section, because a saved component may already
  be there and on brand.
- `list_sections` then `get_section` before editing part of a page.
- `repair_page` if a page they built earlier looks broken.

## Skills in this folder

`.claude/skills/` holds five recipes. Use them rather than improvising:

- **set-up-my-brand** when there is no Style Guide yet.
- **build-a-page** for a new page from a description.
- **copy-a-design** when they hand you a screenshot, HTML, or a web address.
- **edit-a-section** to change part of an existing page.
- **check-a-page** to look at a page and fix what is wrong.
