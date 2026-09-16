---
name: check-a-page
description: Look at a page in a browser at desktop and phone width, say what is wrong in plain words, and fix it. Use after building or editing anything, and whenever the person asks how a page looks or says something looks off.
---

# Check a page

You have not finished until you have looked at it. A tool returning success is not a check.
Reading the layout back is not a check either.

## Recipe

1. **Get the address.** The page URL from `create_page`, or from `list_pages`.
   A draft page is not public: only a browser logged in to WordPress can see it. So the person
   picks one of three ways. They log in to WordPress themselves in the browser window you open,
   and you carry on in that window. Or they open the preview themselves and send you a
   screenshot. Or they ask you to publish the page. You never type their password and you never
   go to the login page on their behalf. If they have the page open in Beaver Builder,
   `get_connected_page` tells you so, and your edits show on their canvas within seconds.

2. **Open it in a browser, twice.**
   - 1280 pixels wide, for desktop.
   - 375 pixels wide, for a phone.
   Use a browser. If you have no way to open one, ask the person to look and describe what they
   see, or to send you a screenshot. Never fetch the page with curl, wget, fetch, the WebFetch
   tool or a script: that gives you markup, not a judgement, and it is not allowed here.

3. **Look for these, in this order.**
   - Can you read every piece of text against what is behind it.
   - Does anything overlap, or sit on top of something else.
   - Does the page scroll sideways, or does anything run off the edge, especially at 375.
   - Are the images actually showing, or are they blank, stretched or squashed.
   - Do the buttons look like buttons, and is their text readable.
   - Is the spacing between sections even, or is one section crammed and another empty.
   - Does it look like one brand, or like two different sites stitched together.
   - At phone width, has anything stayed in a row that should have stacked.

4. **Say what is wrong in plain words.** One line per problem, describing what a visitor would
   see. "The white heading is on a pale background and you cannot read it." Not a list of
   settings.

5. **Fix it through the tools.** The edit-a-section skill covers which tool to use. Colours,
   backgrounds and spacing on a section are `edit_row`. One heading, image or button is
   `edit_module`. If the page looks broken in a way you cannot place, `repair_page` is worth a
   try on a page built some time ago.

6. **Look again.** After each round of fixes, reopen the page at both widths. Repeat until it
   is clean, or until you are down to something you cannot fix, which you then explain.

7. **Report.** What you looked at, what was wrong, what you fixed, and anything still open.

## The hard rule

Never use curl, wget, fetch, the WebFetch tool, a script or any other direct request against
the site, for reading or for writing. The plugin's tools are the only way to read or change it, and a browser is the
only way to look at it.
