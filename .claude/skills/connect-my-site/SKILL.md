---
name: connect-my-site
description: Connect Claude to the person's WordPress site through the BeaverForge AI plugin, or confirm that it is already connected. Use when they say set up my BeaverForge connection, connect my site, connect to WordPress, or when no BeaverForge tools are available.
---

# Connect my site

Check first. Most of the time the connection is already there and there is nothing to do.

## 1. Check whether it is already connected

Call `list_pages`.

- **It returns a list of pages.** The connection already exists. Say so in one line, name a
  couple of the pages you can see so they know it is their site, and stop. Do not offer setup,
  do not touch any configuration file, do not ask for a key.
- **There is no such tool at all, or it fails to connect.** Carry on to step 2.
- **It refuses with a reason** (for example the licence is not active, or the key is not
  valid). The connection exists but the site is turning it down. Pass the reason on in plain
  words and stop. Setting it up again will not fix a refusal.

If there is more than one BeaverForge server configured, more than one site is connected. Ask
which one they mean before building anything.

If `list_pages` works but a second `beaverforge` connection from the installed plugin shows as
failed, that is only the plugin's own entry with no address set. Their site is fine. Tell them
they can set `BFAI_MCP_URL` and `BFAI_MCP_KEY` to the same address and key their working
connection uses, so both point at the same site, and carry on either way.

## 2. Switch the server on, on their site

Talk them through this one step at a time and wait after each step.

In WordPress admin: open the **BeaverForge AI** menu, and on the page headed **BeaverForge AI
Settings** find the **MCP Server** section, then tick **Enable MCP endpoint**. Ask them to
copy the **Endpoint URL** shown just below it. It looks like
`https://their-site.com/wp-json/beaverforge-ai/v1/mcp`. If there is no **MCP Server** section
on that page, the licence is not active yet.

## 3. Create a key

On the same screen, under **Your key**: type a **Label** (for example "Claude Code, work
laptop"), leave **Expiry** blank unless they want one, press **Create key**. The key is shown
once, so tell them to copy it now. It starts with `bfai_`.

**Never ask them to paste the key into the chat, and never type a real key into a file
yourself.**

## 4. Put the endpoint and the key where Claude can read them

Which of these two applies depends on how they started.

**They installed the BeaverForge plugin for Claude Code** (the `/plugin` route, which works in
any folder). The plugin already declares the connection; it reads the address and the key from
two environment variables on their machine. Ask them to add these two lines to their shell
profile themselves (`~/.zshrc` on a Mac, `~/.bashrc` on most Linux machines), with their own
endpoint and their own key:

```bash
export BFAI_MCP_URL="https://their-site.com/wp-json/beaverforge-ai/v1/mcp"
export BFAI_MCP_KEY="bfai_their_key"
```

Then a new terminal, and start Claude Code again.

If they would rather not use environment variables, they can add the server directly instead,
once, for every folder:

```bash
claude mcp add beaverforge --scope user -- npx -y mcp-remote@latest https://their-site.com/wp-json/beaverforge-ai/v1/mcp --header "Authorization:Bearer bfai_their_key" --transport http-only
```

They run that themselves, with their own address and key, so the key never goes through the
chat.

**They cloned the starter folder.** Copy `.mcp.json.example` to `.mcp.json` in the folder, and
ask them to paste their endpoint URL and their key into it themselves, in their editor.
`.mcp.json` is ignored by git, so the key stays on their machine.

## 5. Restart

Claude Code reads connections at startup. Fully quit and reopen it. A reload is not enough. On
the clone route, the first launch after that asks them to approve this project's `.mcp.json`,
so tell them to expect the prompt and say yes.

## 6. Confirm

In the new session, call `list_pages`. A list of their pages means the connection works.

If the tools are still not there: the restart did not happen, the approval prompt was
declined, the environment variables were set in one terminal but Claude Code was started from
another, or there is a typo in the address or the key.

**If it hangs:** almost always an out of date Node. Ask them to run `node -v`. Below 20.18.1
needs an update, then a full restart of Claude Code.

## Claude Desktop

Same endpoint, same key, same command. The settings live in the desktop app's own config file.
The reliable way in is the app itself: **Settings > Developer > Edit Config**. The file is
`claude_desktop_config.json`, normally at
`~/Library/Application Support/Claude/claude_desktop_config.json` on a Mac and
`%APPDATA%\Claude\claude_desktop_config.json` on Windows. Paste the same block that is in
`.mcp.json.example`, then fully quit and reopen the app.
