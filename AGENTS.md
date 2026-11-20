# Instructions for agents working in this repository

This public repository holds the Tolstoy MCP listing for several clients at once. Claude, Cursor, the MCP Registry, Glama and other public directories read the default branch (`main`), so every merge goes live for all of them. A change must not break any of them.

## Read the provider rules first

Before you change the file tree or a manifest, read the current rules. Don't rely on a copy of them here or in the README.

- Claude plugin directory:
  - [Submit a plugin](https://claude.com/docs/plugins/submit)
  - [Pre-submission checklist](https://claude.com/docs/plugins/pre-submission-checklist)
  - [Plugins reference](https://code.claude.com/docs/en/plugins-reference)
  - [Anthropic Software Directory Policy](https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy)
  - The latest finding for this plugin in the Claude directory portal. It names the current allowed-file rule and anything it refused.
- Cursor Marketplace: [Plugins reference](https://cursor.com/docs/reference/plugins) and the [plugin schema](https://raw.githubusercontent.com/cursor/plugins/main/schemas/plugin.schema.json).
- MCP Registry: [registry docs](https://registry.modelcontextprotocol.io/docs) and the [registry repository docs](https://github.com/modelcontextprotocol/registry/tree/main/docs).
- Glama: [server listing](https://glama.ai/mcp/servers/GoTolstoy/mcp) and the [`glama.json` schema](https://glama.ai/mcp/schemas/server.json).

## Which files each client reads

| Client | Reads |
| --- | --- |
| Claude plugin directory | `.claude-plugin/plugin.json`, `.mcp.json`, `skills/`, and the rest of the repository, because the plugin folder is the root |
| Cursor Marketplace | `.cursor-plugin/plugin.json`, `mcp.json`, `skills/`, `cursor/`, `rules/`, and the logo the manifest names |
| MCP Registry | `registry/*.server.json`, published manually by `.github/workflows/publish-mcp-registry.yml` |
| Glama | `glama.json` |
| Cline and other MCP directories | `README.md`, `llms-install.md`, `mcp.json` |

The MCP server itself is `https://apilb.gotolstoy.com/mcp/v1/mcp`. Nothing in this repository deploys it.

## Structure decisions

- **The Claude plugin is the repository root.** That was set when the plugin was submitted, and changing it means a new submission. The directory checks every file in the repository, so any file you add must meet the Claude directory rules above, even if only Cursor or a registry uses it.
- **One repository serves both plugins.** The Cursor and Claude submissions both point at `GoTolstoy/mcp`. Moving either one means a new store submission.
- **`skills/` at the root is shared.** Claude Code loads `skills/` and `agents/` from the plugin root, and the Cursor manifest also lists `skills/`. Put a skill there only if both clients should ship it.
- **Cursor-only files live under `cursor/`, `rules/` and `.cursor-plugin/`.** Cursor-only skills and agents go in `cursor/skills/` and `cursor/agents/`, never in a root `agents/` or `skills/`. Use a rule file format that both Cursor and the Claude directory accept.
- **Registry manifests stay at `registry/*.server.json`.** The publish workflow reads those paths.

## Before merging

1. Read the sources above for every client the change touches. Check that the change doesn't break any client in the table.
2. Claude: run `claude plugin validate ./`, and check every tracked file against the directory's current rules.
3. Cursor: validate the manifest against the schema, then check that every path in it exists:
   ```sh
   curl -fsSLo /tmp/cursor-plugin.schema.json https://raw.githubusercontent.com/cursor/plugins/main/schemas/plugin.schema.json
   npx --yes --package ajv-cli@5 --package ajv-formats@3 ajv validate --spec=draft7 -s /tmp/cursor-plugin.schema.json -d .cursor-plugin/plugin.json -c ajv-formats
   for p in $(jq -r '[.logo,.skills,.agents,.rules,.mcpServers]|flatten|.[]' .cursor-plugin/plugin.json); do test -e "$p" || echo "missing $p"; done
   ```
4. JSON: `jq empty .mcp.json mcp.json glama.json registry/*.json .claude-plugin/plugin.json .cursor-plugin/plugin.json`.
5. Versions: raise `version` in `.claude-plugin/plugin.json` or `.cursor-plugin/plugin.json` only when that plugin's content changes, or when a provider needs a new version. Record the change in `CHANGELOG.md`; history belongs there and in pull requests, not in this file.
6. After merging, check the latest Claude portal finding once it has scanned the new commit.

## Wording

- Describe `run_agent` truthfully. It reaches the platforms a brand connected in Tolstoy (Settings > Connectors). It isn't one direct tool per platform.
- No test-status lines in public files.
- The Cursor description lists the connected platforms first.
