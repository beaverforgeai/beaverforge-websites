---
name: beaverforge-rules
description: How to work on a WordPress site through the BeaverForge AI tools, the order of operations, the rules of engagement and what counts as verification. Read this first on any request about BeaverForge, Beaver Builder, a Style Guide, a page, a section, a module, a saved component, a site menu, a header or footer, or any request to build, edit, copy, check or look at a page on the person's website.
---

# Working on this website with BeaverForge AI

The person you are working with owns a WordPress site built with Beaver Builder. The
BeaverForge AI plugin on that site publishes a set of tools to you. Those tools are how you
read and change the site.

What the tools give you: the brand, whole pages, single sections, single modules, saved
components, menus, the site header and footer, WooCommerce setup, and recreating a design
from a screenshot, from HTML, or from a web address, which you open in the browser and
screenshot first. You do not need to know how any of it works inside. You describe what you
want in the shape the tools ask for, and the plugin builds it.

If you cannot see any BeaverForge tools at all, the connection is not set up yet. Give the
person the three steps under "Connecting your site" below and stop.

## Order of operations

1. **Load the brand first.** Call `get_design_tokens` before you build or edit anything, and
   apply what it returns to every section. If it comes back with `configured: false`, there is
   no brand yet: offer to set one up (see the set-up-my-brand skill) or say clearly that the
   result will not be on brand.
2. **Learn the shape before you write it.** Call `get_module_schema("section")` for the
   section structure, and `get_module_schema("<slug>")` for each module you are about to use.
3. **Build or edit.** One page at a time, one section at a time.
4. **Look at the result in a browser, if they let you.** Ask once, the first time there is
   something to see, whether you may open the page in a browser to check your work; then do what
   they said for the rest of the session. Yes: look at desktop and phone width after every change.
   No, or no browser here: say so once, read your work back with the tools, and never ask again.

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

Looking at what you built is part of the work, especially design work, and it needs the
person's say-so. So you ask ONCE per session, in one line ("I'd like to open the page in a
browser to check my work. Is that all right?"), and you take the answer:

- **Yes.** For every page you build or change from then on, without asking again: open the page
  URL in a browser at 1280 wide and again at 375 wide; check the text is readable against its
  background, nothing overlaps, nothing overflows sideways, images are actually showing, buttons
  look like buttons, and the spacing between sections is even; say what you saw; if something is
  wrong, fix it through the tools and look again.
- **No, no answer, or no browser in this session.** Say so once, plainly. Then do not ask again,
  do not end your messages with "please check it", and do not ask them to look or to send a
  screenshot. Read each section back with `get_section` after you write it, and say once in your
  final report that you have not seen the page rendered.

A draft page is not public: only a browser that is logged in to WordPress can see it. So if they
said yes, they log in themselves in the browser window you open, or they ask you to publish the
page first. You never type their password and you never go to the login page on their behalf.

If they are editing the page in Beaver Builder right now, `get_connected_page` tells you so,
and your edits appear on their canvas within seconds rather than on the public address.

"The tool returned success" is not verification. Reading the layout back is not verification
either. Seeing it is.

## Connecting your site

This is a one-time setup the person does themselves, outside this project. Already connected
it? Skip this step.

**1. Get your address and your key.**
In WordPress admin, open the **BeaverForge AI** menu. On the page headed **BeaverForge AI
Settings**, find the **MCP Server** section. Tick **Enable MCP endpoint** and copy the
**Endpoint URL**. Then under **Your key**, type a label (for example "Claude Code, work
laptop"), press **Create key**, and copy the key straight away, because it is shown only once.

**2. Run this one command in a terminal**, once, with your own address and your own key in
place of the two placeholders. It works in every folder afterwards.

```bash
claude mcp add beaverforge --scope user -- npx -y mcp-remote@latest https://your-site.com/wp-json/beaverforge-ai/v1/mcp --header "Authorization:Bearer bfai_your_key" --transport http-only
```

**3. Restart Claude Code.** Fully quit and reopen it. A reload is not enough.

Claude Desktop takes the same address and the same key, put into the desktop app's own MCP
settings instead.

**The rule for Claude:** if the BeaverForge tools are not available, tell the person those
three steps and stop. Never ask for their key, never write or edit a configuration file for
them, and never try to connect by any other means. If the tools are available, carry on.

## Handy starting points

- `list_pages` to see what exists, `list_unbuilt_pages` for older pages not yet built with
  Beaver Builder, which you then adopt with `enable_builder` before any layout tool will work
  on them, `list_posts` for blog posts and other content types.
- `get_connected_page` when they say "this page" or "the page I have open".
- `list_components` before building a common section, because a saved component may already
  be there and on brand.
- `list_sections` then `get_section` before editing part of a page.
- `repair_page` if a page they built earlier looks broken.

## The other skills here

Use these recipes rather than improvising:

- **set-up-my-brand** when there is no Style Guide yet.
- **build-a-page** for a new page from a description.
- **copy-a-design** when they hand you a screenshot, HTML, or a web address.
- **edit-a-section** to change part of an existing page.
- **check-a-page** to look at a page and fix what is wrong.
