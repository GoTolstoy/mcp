---
name: tolstoy-social-video
description: Work with Instagram, Pinterest, YouTube, TikTok and X through Tolstoy, after the brand connects them in Tolstoy under Settings > Connectors. Use when the user asks about posts, comments, account insights or publishing on Instagram, Pinterest, YouTube, TikTok or X (Twitter). Requests go to the Tolstoy Agent through the run_agent tool.
---

# Social and video platforms through Tolstoy

Tolstoy reaches Instagram, Pinterest, YouTube, TikTok and X through the Tolstoy Agent, not through a separate
tool for each platform. Follow the `tolstoy-connectors` skill for every request:
check that `run_agent` is available, make sure the brand connected the platform in
Tolstoy under **Settings > Connectors**, send the request with `run_agent`, and read
the answer with `get_agent_chat`.

| Platform | What the Tolstoy connector covers | Tested through run_agent |
| --- | --- | --- |
| Instagram | account metrics, post and carousel insights, comment moderation, content publishing | Not tested through run_agent yet |
| Pinterest | account insights, boards, pins and top pins, creating pins | Not tested through run_agent yet |
| YouTube | channel overview and analytics, video insights, transcripts, comments, playlists | Not tested through run_agent yet |
| TikTok | account metrics, video insights, content pull, posting | Not tested through run_agent yet |
| X (Twitter) | organic posts, and X Ads when the X connection granted ads access | Returned thin data in a test |

The middle column lists the areas each Tolstoy connector is built for. It does not
promise that every request returns data. Where a platform is untested, say so when
you report its answer, and check the result in the platform itself when it matters.

## Ask well

- Name the platform, the account or store, and the date range in the `run_agent`
  message, in the user's own words.
- Ask for one platform per turn. Compare platforms in your own reply, and keep each
  number with its platform and date range.
- A value the agent could not read is "not available", never 0.

## Before any change

Sending, publishing, replying, changing a status or budget, or editing records changes
something outside Tolstoy. Show the user exactly what will change and get an explicit
yes before you ask the Tolstoy Agent to do it, then have the agent read the result back.
