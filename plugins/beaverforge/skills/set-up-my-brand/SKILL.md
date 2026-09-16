---
name: set-up-my-brand
description: Set up the site's Style Guide, the brand colours, fonts, buttons and spacing everything else is built from. Use when there is no brand yet, when get_design_tokens comes back with configured false, or when the person asks for a new look, a restyle or a rebrand.
---

# Set up my brand

The Style Guide is the site's brand. Every page you build afterwards reads from it, so set it
up before building anything.

## Recipe

1. **Check what is there.**
   `get_design_tokens`
   If `configured` is true there is already a brand. Show them the palette and fonts and ask
   whether they want to keep it or replace it. Replacing a brand changes the whole site, so do
   not do it without a clear yes.

2. **Ask the questions the plugin wants asked.**
   `get_onboarding_questions`
   It hands back the questions to ask before a brand is set up, in the order to ask them. Ask
   them conversationally, one or two at a time. Do not invent answers.

3. **Offer the industry list.**
   `get_industries`
   It hands back the industries the plugin recognises, grouped by category. Ask which one fits
   best and keep the exact key. Use `custom` only if nothing fits.

4. **Design it.**
   `generate_design_tokens` with a short `brief` describing the business and the mood, plus an
   optional `style_direction` such as "warm and rustic" or "modern minimal". Describe what the
   business does, not the business name. This takes up to a minute.

5. **Show it and wait.**
   Summarise what came back in plain words: the colours, the two fonts, the overall feel.
   Nothing is saved yet. If they want a different direction, run step 4 again with a different
   `style_direction`. Repeat until they say yes.

6. **Save it, only on their approval.**
   `save_design_tokens` with the complete `tokens_v2` object that came back.
   Then `save_brand_identity` with `business_name` and the `industry` key. For a brand new
   site, pass `set_wp_title: true` so the site title matches, and pass a `tagline` if they gave
   you one.

7. **Offer to redraw the header and footer.**
   Building pages does not rebrand the site header and footer. If they want those to match,
   `rebuild_site_chrome` does it. It needs two things in place first: Beaver Themer active on
   the site, and a Style Guide already saved, which is step 6. It also overwrites the existing
   header and footer including any hand edits. Say that out loud and wait for a yes before
   calling it.

8. **Look at it.** Follow the check-a-page skill on the home page, or on any page, so they can
   see the brand on something real.

## Notes

- Never save a brand the person has not seen and approved.
- If they ask for one specific colour or font, follow them and say which part of the generated
  brand you overrode.
- The tools are the only way to change the site. Never use curl, wget, fetch or any script
  against the site.
- What each tool does is written on the tool itself, and that description arrives with the
  connection. Read it there. The summaries here are only a route map.
