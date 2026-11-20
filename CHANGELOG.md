# Changelog

## 1.2.6 (Claude) - 2026-11-20

- AGENTS.md and README link to each provider's rules instead of restating them.
- AGENTS.md: every file in the repository is part of the Claude plugin, so a file added for another client is checked against the Claude directory's file rules before merging.
- README and CHANGELOG no longer write image paths in backticks, which the Claude directory flagged.
- AGENTS.md: how to add another store without breaking the Claude or Cursor plugin, with links to OpenAI, Gemini CLI and Agent Plugins docs.
- AGENTS.md, README and CHANGELOG no longer name image file paths or show download-and-run commands; the Claude directory holds a version for either. CLAUDE.md is removed, because the directory warns that it isn't loaded at the plugin root; AGENTS.md is the agent guide.
- Claude 1.2.6, so the directory checks the docs fixes as a new version.

## 1.2.5 (Claude) - 2026-11-20

- Removed the SVG logo; Anthropic's directory accepts an SVG only as the plugin's icon. The PNG logo is the same image and stays the icon for Claude, the MCP Registry and the README. Cursor's icon is unchanged.
- AGENTS.md now states the directory's file policy.

## 1.3.1 (Cursor) and 1.2.4 (Claude) - 2026-11-20

- The Cursor rule is now `rules/use-tolstoy.md`, the `.md` form Cursor also reads, so the repository has no `.mdc` file. Its text is unchanged.
- README: which files each client reads.

## 1.3.0 - 2026-11-19

Cursor plugin:

- The description says what Tolstoy does (images and videos from the store's products, the media library, store analytics) and names the platforms the Tolstoy Agent reaches once a brand connects them in Tolstoy. The keywords name those platforms, what brands ask for, and Tolstoy's own product.
- New skill `cursor/skills/tolstoy-connectors`, which reaches connected platforms through `run_agent` and lists what each connector covers. The Cursor plugin ships it with the existing `ecommerce-analytics` and `tolstoy-product-media` skills.
- New always-on rule `rules/use-tolstoy.md` (first shipped as `.mdc`) and agent `cursor/agents/tolstoy-commerce-agent.md`. The rule routes requests for the brand's own data or actions in a connected platform to `tolstoy-connectors` and `run_agent`, leaves Tolstoy's own tools as they are, and excludes code that integrates with a platform, general questions about a platform, and platforms the client has its own connector for.
- The manifest points at its skills (`skills/` and `cursor/skills/`), rules, agent and the root `mcp.json` (`type: http`). `.cursor-plugin/mcp.json` is removed.
- A 512 by 512 PNG listing icon.
- Added `SECURITY.md` and this changelog.

The Claude plugin (`.claude-plugin/plugin.json`, `.mcp.json`, `skills/`) is unchanged.

## 1.2.3

- `ecommerce-analytics` skill, and analytics in the plugin listings.

## 1.0.0

- Initial Cursor Marketplace plugin: the Tolstoy workspace MCP server over OAuth.
