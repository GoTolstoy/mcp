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
- Possible future stores:
  - OpenAI plugins for ChatGPT and Codex: [package](https://developers.openai.com/plugins/build/plugins) and [submit](https://developers.openai.com/plugins/deploy/submission).
  - Gemini CLI extensions: [reference](https://geminicli.com/docs/extensions/reference/) and [release](https://geminicli.com/docs/extensions/releasing/).
  - The [Agent Plugins](https://agent-plugins.org) standard.

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

- **The Claude plugin is the repository root.** That was set when the plugin was submitted, and changing it means a new submission.
- **Every file in the repository is part of the Claude plugin.** A file added for Cursor, a registry or a store is still checked by the Claude directory. Before adding or renaming a file, check its type, its size, and how other files mention it against the [layout](https://claude.com/docs/plugins/pre-submission-checklist#repository-and-folder-layout) and [plugin folder files](https://claude.com/docs/plugins/pre-submission-checklist#files-in-the-plugin-folder) sections of the checklist, and against the latest portal finding. This applies to Markdown too, including how docs refer to images. If a client needs a file the Claude directory won't accept, don't add it here. Raise it with the repository owner instead: the alternative is a Claude plugin in a subfolder, which needs a new Claude submission.
- **One repository serves both plugins.** The Cursor and Claude submissions both point at `GoTolstoy/mcp`. Moving either one means a new store submission.
- **`skills/` at the root is shared.** Claude Code loads `skills/` and `agents/` from the plugin root, and the Cursor manifest also lists `skills/`. Put a skill there only if both clients should ship it.
- **Cursor-only files live under `cursor/`, `rules/` and `.cursor-plugin/`.** Cursor-only skills and agents go in `cursor/skills/` and `cursor/agents/`, never in a root `agents/` or `skills/`. Use a rule file format that both Cursor and the Claude directory accept.
- **Registry manifests stay at `registry/*.server.json`.** The publish workflow reads those paths.

## Adding another store

1. Read that store's docs above and find which files it needs, and where.
2. Check every new file against the Claude directory rules, because it will sit inside the Claude plugin. The rules also cover what text files contain: for example, the directory holds a version for review if a document names an image or font file path, or shows a download-and-run command. Describe files instead, and link to tools' install docs. Store templates often use file types the Claude directory refuses, so check before copying a template file as it is. For example, Cursor's own template uses an `.mdc` rule and an SVG logo.
3. Check whether the new manifest is also read by a client that's already here. Cursor, for example, loads a root `plugin.json` in the Agent Plugins format as well as `.cursor-plugin/plugin.json`. If two clients would read the same path, test both before merging.
4. Prefer packages the store builds from an upload, when it offers one, over committing new files.
5. If a store needs a file the Claude directory won't accept, or needs to own the repository root, stop and raise it with the repository owner. The alternative layout gives each plugin its own subfolder, and that needs a new Claude submission.
6. Add the store to the table above.

## Before merging

1. Read the sources above for every client the change touches. Check that the change doesn't break any client in the table.
2. Claude: run `claude plugin validate ./`. It only checks that files are well-formed ([what it checks](https://claude.com/docs/plugins/pre-submission-checklist)), not the directory's file rules. List the files the change adds, renames or edits (`git diff --name-status origin/main`), and check each one against the checklist sections above and the latest portal finding. For a bigger change, also run the portal's Validate, which reports blocking findings and policy holds without submitting anything.
3. Cursor: validate `.cursor-plugin/plugin.json` against the [Cursor plugin schema](https://raw.githubusercontent.com/cursor/plugins/main/schemas/plugin.schema.json) with a JSON Schema validator such as [ajv-cli](https://ajv.js.org/packages/ajv-cli.html) (draft-07, with formats). Then check that every path in the manifest exists.
4. JSON: check that every `.json` file parses.
5. Versions: raise `version` in `.claude-plugin/plugin.json` or `.cursor-plugin/plugin.json` only when that plugin's content changes, or when a provider needs a new version. Record the change in `CHANGELOG.md`; history belongs there and in pull requests, not in this file.
6. After merging, check the latest Claude portal finding once it has scanned the new commit.

## Wording

- Describe `run_agent` truthfully. It reaches the platforms a brand connected in Tolstoy (Settings > Connectors). It isn't one direct tool per platform.
- No test-status lines in public files.
- The Cursor description lists the connected platforms first.
