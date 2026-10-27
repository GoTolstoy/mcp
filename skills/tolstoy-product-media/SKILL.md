---
name: tolstoy-product-media
description: Find the existing Tolstoy library media for a store product and fill its gaps with the merchant's own uploads. Use when a merchant asks which library media to use for a product, wants to upload media for it, or needs a first useful Tolstoy workflow in Claude or Cursor.
---

# Find and organize product media in Tolstoy

Use the connected merchant workspace. Start with one product or a small collection so the merchant can review a concrete result.

## Confirm the product

1. Find the named product with `search_products`. If the request names no product, ask for one. Use the returned `externalProductId` in later calls and never invent a product ID.
2. If the product is not in the connected store, stop and explain how to reconnect to the intended workspace. If the workspace has no catalog yet, offer `connect_products`.

## Build a shortlist from existing media

3. Use `search_media` to find relevant library media. Use `get_media` to inspect the strongest candidates and their product tags. Start with at most five candidates. A title or tag does not prove what the media shows; use available previews and details, and label any content you cannot inspect.
4. Return a compact table with the product, exact media ID and source, available preview link, the reason it fits, and evidence limits. State whether the merchant has enough suitable media or which gap remains.

## Fill a gap

If suitable media is missing, offer `upload_media_from_panel` for the merchant's own files. A client that can run shell commands can upload a local file with `start_media_upload` and `finish_media_upload`. Read each uploaded item with `get_media` before adding it to the shortlist. Work the tools do not cover happens in the Tolstoy platform.

## Recover from setup problems

- Missing connector: confirm the individual has added and signed in to Tolstoy in this client. Team approval alone does not prove their connection works.
- Wrong workspace: reconnect with the intended Tolstoy workspace, then repeat `search_products`.
- Tool unavailable: inspect the current tool list. Do not retry a missing tool under a guessed name.
- No relevant media: state the gap and offer an upload. Do not create a fictional shortlist.
