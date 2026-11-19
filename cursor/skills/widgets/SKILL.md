---
name: widgets
description: Builds and changes the brand's AI widgets with Tolstoy's widget tools - the storefront widgets, landing pages and app blocks Tolstoy hosts for the store. Use when the user asks to create, find, change, preview or publish an AI widget, or asks what changed in one.
---

## AI widgets

An AI widget is a small web project Tolstoy builds from a template and hosts for the brand: a widget on the store's pages, a landing page, or a block in the store's mobile app. list_widgets gives each widget's widgetId, template and status. The connection reaches the widgets of its own workspace only.

The merchant's agent works on the widget's files through the widget tools; no Tolstoy model runs for them. Platform's widget page and the Tolstoy Agent work on the same files and the same history, so a change made here is what they show.

## The project

Paths are relative to the widget root. AGENTS.md at the root describes the project: how it is built, where its parts live and the rules its code follows. The file list shows none of this, so an answer about a widget or a change to it starts from its AGENTS.md. widget-manifest.json names its plugins and its preview pages. A plugin's code under src/plugins/<pluginId> is a copy of a Tolstoy plugin at the version widget-manifest.json names, which the widget calls like a library; the widget's own code is the rest of the project. A search for how the widget works leaves src/plugins out, and a plugin file is worth reading where the widget's own code calls it. A search shows only the lines that match its words, and most of what code does sits in the lines around them under other names. An answer about how the widget works reads in full the files that do its work, not only the search matches. Most templates are React with Vite and Tailwind, under src/; Shopify Liquid templates keep their markup in .liquid files.

## Changing code

run_widget_command runs a shell command with bash from the widget root, in the sandbox Platform and the Tolstoy Agent use. The sandbox has Node, pnpm, git, ripgrep and fd; commands read, search and change the files, and pnpm add adds a package. The result keeps only the last 2000 lines or 50KB of a command's output, and a head or tail in the command cuts it further, so a command that prints more than fits loses files without an error. Read the files that matter in commands whose whole output fits. When a command changes the widget's files, the tool commits and pushes them as one save in the widget's history, named after the command; a command that changes nothing makes no save. The build happens when the widget is published.

An agent with its own shell and git can instead clone the widget's repository from get_widget_clone_url, change it with its own tools, and commit and push to main; each pushed commit is a save, and the widget tools bring the sandbox up to it before they act. run_widget_command serves a host without a shell.

## Checking a change

preview_widget gives links to the widget's live preview, which runs the current files. get_widget_history lists the saves, and with a sha shows one save's diff.

## Going live

Shoppers see a change only after publish_widget, which builds the widget and replaces its live version. A failed build leaves the live version as it was and returns the build's errors. discard_widget_changes returns the widget to its last published version and removes every later save.
