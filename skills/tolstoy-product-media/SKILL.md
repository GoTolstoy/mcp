---
name: tolstoy-product-media
description: Find existing Tolstoy media for a store product and create new product content with Tolstoy Studio. Use when a merchant asks which library media to use for a product, wants new images or videos for it, or needs a first useful Tolstoy workflow in Cursor.
---

# Find and create product media in Tolstoy

Use the connected merchant workspace. Start with one product or a small collection so the merchant can review a concrete result.

## Confirm the product

1. Find the named product with `search_products`. If the request names no product, ask for one. Use the returned `externalProductId` in later calls and never invent a product ID.
2. If the product is not in the connected store, stop and explain how to reconnect to the intended workspace.

## Build a shortlist from existing media

3. Use `search_media` to find relevant library media. Use `get_media` to inspect the strongest candidates and their product tags. Start with at most five candidates. A title or tag does not prove what the media shows; use available previews and details, and label any content you cannot inspect.
4. Return a compact table with the product, exact media ID and source, available preview link, the reason it fits, and evidence limits. State whether the merchant has enough suitable media or which gap remains.

## Create new content

If the merchant asks for new content, send the request to `run_agent` with the product and the media IDs the merchant chose instead of describing them in words. Keep the returned `chatId` and pass it to continue the same chat. Read the result with `get_agent_chat`. A Studio draft is not published to the store.

## Recover from setup problems

- Missing connector: confirm the individual has added and signed in to Tolstoy in this client. Team approval alone does not prove their connection works.
- Wrong workspace: reconnect with the intended Tolstoy workspace, then repeat `search_products`.
- Tool unavailable: inspect the current tool list. The Library connection does not expose Studio generation. Do not retry a missing tool under a guessed name.
- No relevant media: state the gap. Offer `upload_media_from_panel` for the merchant's own files or Studio generation. Do not create a fictional shortlist.

For client setup, see [the first-workflow guide](../../docs/first-workflow.md).
