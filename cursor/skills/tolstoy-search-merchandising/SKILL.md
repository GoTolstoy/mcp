---
name: tolstoy-search-merchandising
description: Work with Rebuy, Nosto and Klevu through Tolstoy, after the brand connects them in Tolstoy under Settings > Connectors. Use when the user asks about product recommendations, on-site search, collections or merchandising in Rebuy, Nosto or Klevu. Requests go to the Tolstoy Agent through the run_agent tool.
---

# On-site search, recommendations and merchandising through Tolstoy

Tolstoy reaches Rebuy, Nosto and Klevu through the Tolstoy Agent, not through a separate
tool for each platform. Follow the `tolstoy-connectors` skill for every request:
check that `run_agent` is available, make sure the brand connected the platform in
Tolstoy under **Settings > Connectors**, send the request with `run_agent`, and read
the answer with `get_agent_chat`.

| Platform | What the Tolstoy connector covers | Tested through run_agent |
| --- | --- | --- |
| Rebuy | recommendations, search, collections, data sources, analytics | Not tested through run_agent yet |
| Nosto | recommendations, products, orders, customers | Not tested through run_agent yet |
| Klevu | search, product discovery, category merchandising, recommendations | Not tested through run_agent yet |

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
