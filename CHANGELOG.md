# Changelog

## 1.3.0 - 2026-11-19

Cursor plugin:

- The description says what Tolstoy does (images and videos from the store's products, the media library, store analytics) and names the platforms the Tolstoy Agent reaches once a brand connects them in Tolstoy. The keywords name those platforms, what brands ask for, and Tolstoy's own product.
- New skills in `cursor/skills/`: `tolstoy` and `widgets`, the same skills the Tolstoy ChatGPT plugin ships, and `tolstoy-connectors`, which reaches connected platforms through `run_agent` and lists what each connector covers.
- New always-on rule `rules/use-tolstoy.mdc` and agent `cursor/agents/tolstoy-commerce-agent.md`. Both apply only to the brand's own account data or actions in a connected platform, not to code that integrates with a platform.
- The manifest points at its skills (`skills/` and `cursor/skills/`), rules, agent and the root `mcp.json` (`type: http`). `.cursor-plugin/mcp.json` is removed.
- Listing icon `assets/icon.png` (512×512).
- Added `SECURITY.md` and this changelog.

The Claude plugin (`.claude-plugin/plugin.json`, `.mcp.json`, `skills/`) is unchanged.

## 1.2.3

- `ecommerce-analytics` skill, and analytics in the plugin listings.

## 1.0.0

- Initial Cursor Marketplace plugin: the Tolstoy workspace MCP server over OAuth.
