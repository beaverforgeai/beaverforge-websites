# BeaverForge AI starter pack for Claude

This gives Claude Code the know-how to build and edit the Beaver Builder pages on your
WordPress site by chatting with you. Claude never edits your site files. It works through the
tools the BeaverForge AI plugin publishes from your site.

Everything in here is instructions for Claude: how to behave, what order to work in, and
when to stop and ask you. All of the real ability lives in the plugin.

Requires BeaverForge AI 3.0.1.6 or later.

## Two ways to start

Both routes give Claude the same recipes. Route 1 installs them once and they work in every
folder on your computer. Route 2 keeps everything in one folder you can edit.

### Route 1: install it as a Claude Code plugin (recommended, no cloning)

Run these two commands in a terminal:

```bash
claude plugin marketplace add beaverforgeai/beaverforge-websites
claude plugin install beaverforge@beaverforge-websites
```

Then start Claude Code (`claude`) in whichever folder you like, and say:

> set up my BeaverForge connection

Claude checks first whether your site is already connected. If it is, it says so and stops. If
it is not, it talks you through switching the plugin's MCP server on in WordPress, creating
your key, and setting two lines in your shell profile so every folder can use them:

```bash
export BFAI_MCP_URL="https://your-site.com/wp-json/beaverforge-ai/v1/mcp"
export BFAI_MCP_KEY="bfai_your_key"
```

You put your own key in yourself. Never paste it into the chat. Open a new terminal afterwards
so the two lines are in effect, and start Claude Code again.

If you would rather not use environment variables, add the server directly instead, once, for
every folder:

```bash
claude mcp add beaverforge --scope user -- npx -y mcp-remote@latest https://your-site.com/wp-json/beaverforge-ai/v1/mcp --header "Authorization:Bearer bfai_your_key" --transport http-only
```

### Route 2: clone this folder

**1. Switch the plugin's MCP server on.**
In WordPress admin, open the **BeaverForge AI** menu. On the page headed **BeaverForge AI
Settings**, find the **MCP Server** section. Tick **Enable MCP endpoint**. Copy the
**Endpoint URL**. Then under **Your key**, type a label (for example "Claude Code, work
laptop") and press **Create key**. Copy the key straight away, because it is shown once.
If there is no **MCP Server** section on that page, the licence is not active yet.

**2. Clone this folder and open Claude Code in it.**

```bash
git clone https://github.com/beaverforgeai/beaverforge-websites.git my-site-with-claude
cd my-site-with-claude
claude
```

**3. Ask Claude to finish the setup.**
Say:

> set up my BeaverForge connection

Claude will talk you through it: copy `.mcp.json.example` to `.mcp.json`, put your endpoint
and key into it, restart Claude Code, then list your pages to prove the connection works.
Keep the key in the file. Do not paste it into the chat.

The connection file lists a second server as well, `playwright`. That is the browser Claude
opens to look at your pages with its own eyes; it installs itself the first time it runs and
needs nothing from your site. The plugin route brings the same browser with it.

Claude Desktop users can follow the same setup section. Claude will give you the desktop
variant if you ask for it.

## Already have the MCP set up?

Then there is nothing to connect. The recipes use whichever BeaverForge server is already
configured on your machine, under whatever name you gave it. Install the plugin, or clone the
folder, and start asking for pages.

If you ask Claude to set up the connection anyway, it calls `list_pages` first, sees your
pages, tells you the connection already exists and stops, without touching your setup. If you
have more than one site connected, say which one you mean before asking for work.

One detail worth knowing on route 1: the plugin brings a `beaverforge` connection of its own,
and until `BFAI_MCP_URL` and `BFAI_MCP_KEY` are set it shows in `/mcp` as failed to connect.
Set the two variables to the same address and key your existing connection uses and both point
at the same site. Your own connection keeps working either way, and Claude uses it.

## What Claude will then do for you

- Set up your brand once, the Style Guide, so everything it builds afterwards matches it.
- Build a new page from a description, section by section, and show you the result.
- Recreate a design you hand it: a screenshot, HTML, or a design from a web address, which
  Claude opens in the browser and screenshots before rebuilding it.
- Edit one section of an existing page without disturbing the rest.
- Check a page at desktop and phone width and fix what looks wrong.
- Place your saved components, build menus, and set up a WooCommerce store.

Ask in plain words. "Build me a services page for a plumbing business", "make that hero
section darker", "recreate this page for me", "check the home page on a phone".

## Working with Claude Design

If you want to see a page before it is built, mock it up in Claude Design first. Ask for the
layout you have in mind, adjust it on the canvas until you like it, then export or screenshot
the artboard and hand that image to Claude with "recreate this". That runs the copy-a-design
skill in this folder, and you end up with a real, editable Beaver Builder page that matches
the mock-up.

## The one hard rule

Claude must only touch your site through the plugin's tools, and only look at it through a
browser. No `curl`, no `wget`, no scripts, no WebFetch tool, no direct requests to your site.
If you ever see Claude reach for one of those, stop it and point it back at this rule.

## The files in here

| File | What it is |
|---|---|
| `CLAUDE.md` | Claude reads this automatically when you clone the folder. How to behave, and how to set up the connection. |
| `.mcp.json.example` | The template for your connection. Copy it to `.mcp.json` and fill in your details. |
| `.mcp.json` | Your real connection, with your key in it. Never committed to git. |
| `.gitignore` | Keeps your key and local clutter out of git. |
| `.claude/skills/` | Six recipes: connect my site, set up my brand, build a page, copy a design, edit a section, check a page. |
| `.claude-plugin/marketplace.json` | What route 1 reads when you add this repository as a marketplace. |
| `plugins/beaverforge/` | The same recipes packaged as a Claude Code plugin, plus the connection it declares. Route 1 installs this. |

You can edit any of it. If Claude does something you would rather it did differently, tell it,
and ask it to write the preference into `CLAUDE.md` so it sticks.
