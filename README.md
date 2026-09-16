# BeaverForge AI websites for Claude

This gives Claude Code the know-how to build and edit the Beaver Builder pages on your
WordPress site by chatting with you. Claude never edits your site files. It works through the
tools the BeaverForge AI plugin publishes from your site.

Everything in here is instructions for Claude: how to behave, what order to work in, and
when to stop and ask you. All of the real ability lives in the plugin.

Requires BeaverForge AI 3.0.1.6 or later.

## Connect your site (once)

You do this yourself, once, and it then works everywhere. Already connected it? Skip this
step.

**1. Get your address and your key.**
In WordPress admin, open the **BeaverForge AI** menu. On the page headed **BeaverForge AI
Settings**, find the **MCP Server** section. Tick **Enable MCP endpoint** and copy the
**Endpoint URL**. Then under **Your key**, type a label (for example "Claude Code, work
laptop"), press **Create key**, and copy the key straight away, because it is shown only once.
If there is no **MCP Server** section on that page, your licence is not active yet.

**2. Run this one command in a terminal**, once, with your own address and your own key in
place of the two placeholders. It works in every folder afterwards.

```bash
claude mcp add beaverforge --scope user -- npx -y mcp-remote@latest https://your-site.com/wp-json/beaverforge-ai/v1/mcp --header "Authorization:Bearer bfai_your_key" --transport http-only
```

**3. Restart Claude Code.** Fully quit and reopen it. A reload is not enough.

Claude Desktop users: the same address and the same key go into the desktop app's own MCP
settings instead.

## Install the skills

Both routes give Claude the same recipes. Route 1 installs them once and they work in every
folder on your computer. Route 2 keeps everything in one folder you can edit.

### Route 1: install it as a Claude Code plugin (recommended, no cloning)

Run these two commands in a terminal:

```bash
claude plugin marketplace add beaverforgeai/beaverforge-websites
claude plugin install beaverforge@beaverforge-websites
```

Then start Claude Code (`claude`) in whichever folder you like and start asking for pages.

### Route 2: clone this folder

```bash
git clone https://github.com/beaverforgeai/beaverforge-websites.git my-site-with-claude
cd my-site-with-claude
claude
```

Claude reads `CLAUDE.md` and the recipes in `.claude/skills/` automatically when you start it
in that folder.

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
skill, and you end up with a real, editable Beaver Builder page that matches the mock-up.

## The one hard rule

Claude must only touch your site through the plugin's tools, and only look at it through a
browser. No `curl`, no `wget`, no scripts, no WebFetch tool, no direct requests to your site.
If you ever see Claude reach for one of those, stop it and point it back at this rule.

## The files in here

| File | What it is |
|---|---|
| `CLAUDE.md` | Claude reads this automatically when you clone the folder. How to behave, and how the connection is made. |
| `.gitignore` | Keeps your keys and local clutter out of git. |
| `.claude/skills/` | Five recipes: set up my brand, build a page, copy a design, edit a section, check a page. |
| `.claude-plugin/marketplace.json` | What route 1 reads when you add this repository as a marketplace. |
| `plugins/beaverforge/` | The same recipes packaged as a Claude Code plugin, plus the house rules. Route 1 installs this. |

You can edit any of it. If Claude does something you would rather it did differently, tell it,
and ask it to write the preference into `CLAUDE.md` so it sticks.
