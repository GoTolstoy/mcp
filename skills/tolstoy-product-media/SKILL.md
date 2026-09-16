---
name: tolstoy-product-media
description: Find existing Tolstoy videos for a store product and prepare a useful product-page media shortlist. Use when a merchant asks which library assets to use for a product, wants to check its current shoppable widget, or needs a first useful Tolstoy workflow in Cursor.
---

# Find product media in Tolstoy

Use the connected merchant workspace. Start with one product or a small collection so the merchant can review a concrete result.

## Confirm the workspace and product

1. Call `get_setup_state` with `include: ["brand", "catalog", "integrations", "stores"]`. Read the returned brand, store domain, and `unavailable` sections. A failed read means unknown, not an empty account.
2. Compare that store with the merchant's request. If it is a different workspace, stop and explain how to reconnect. If several stores match, ask the merchant to select one. Use the returned store domain and IDs in later calls.
3. Find the named product with `search_products` or `browse_products`. If the request names no product, ask for one or show a short selection from the catalog. Never invent a product ID or infer a merchant's private catalog from the public Shopper server.

## Build a shortlist from existing media

4. Use `search_assets` to find relevant library assets. Use `get_asset` to inspect the strongest candidates and their existing product tags. Start with at most five candidates. Do not imply a title or tag proves what the video shows; use available previews and details, and label any content you cannot inspect.
5. When the task includes current placement, use `list_widgets` and `get_widget` for the selected store and product. Report the returned live or draft state. A matching tag does not prove the asset is on the live product page.
6. Return a compact table with the product, exact asset ID, available preview link, reason it fits, evidence limits, and current placement if checked. State whether the merchant has enough suitable media or which specific gap remains.

## Complete the requested action

If the merchant requested a shortlist, that is the deliverable. If the merchant also requested a tag or widget change, execute only that authorized change using the discovered tool schema, then read back the affected asset or widget. Describe the exact before and after state. Changing a live widget can affect the storefront; a request to explore options does not authorize publication.

Keep generation and paid ads out of this existing-media workflow unless the merchant separately requests them. Do not claim a sale, performance improvement, published placement, or customer adoption from a successful tool call alone.

## Recover from setup problems

- Missing connector: confirm the individual has added and signed in to Tolstoy in this client. Team approval alone does not prove their connection works.
- Wrong workspace: reconnect with the intended Tolstoy workspace, then repeat `get_setup_state`.
- Catalog importing: report its current import status and resume when products are available.
- Integration needs attention: name the returned service and reconnect it through the supported tool or Tolstoy settings before retrying dependent work.
- No relevant media: state the gap and ask the merchant which existing asset or source to use. Do not create a fictional shortlist.
- Tool unavailable: inspect the current tool list. Library-only connections do not expose Studio generation or paid ads. Do not retry a missing tool under a guessed name.

For client setup and a repeat task, see [the first-workflow guide](../../docs/first-workflow.md).
