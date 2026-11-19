---
name: tolstoy-email-sms
description: Work with Klaviyo, Attentive, Postscript and Drip through Tolstoy, after the brand connects them in Tolstoy under Settings > Connectors. Use when the user asks about email or SMS campaigns, subscribers, segments or messaging in Klaviyo, Attentive, Postscript or Drip. Requests go to the Tolstoy Agent through the run_agent tool.
---

# Email and SMS through Tolstoy

Tolstoy reaches Klaviyo, Attentive, Postscript and Drip through the Tolstoy Agent, not through a separate
tool for each platform. Follow the `tolstoy-connectors` skill for every request:
check that `run_agent` is available, make sure the brand connected the platform in
Tolstoy under **Settings > Connectors**, send the request with `run_agent`, and read
the answer with `get_agent_chat`.

| Platform | What the Tolstoy connector covers | Tested through run_agent |
| --- | --- | --- |
| Klaviyo | campaigns, campaign drafts, segments, events | Returned real data in a test |
| Attentive | subscribers, offers, product catalog, ecommerce events, privacy requests | No campaign reporting |
| Postscript | SMS messaging, subscribers, compliance events | Not tested through run_agent yet |
| Drip | email campaign drafts, test emails, audiences, campaign results | Not tested through run_agent yet |

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
