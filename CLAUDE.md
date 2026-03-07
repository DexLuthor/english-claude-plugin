# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Claude Code plugin that provides English grammar tools. It exposes three slash commands (`/english:fix-grammar`, `/english:insights`, and `/english:reset-history`) and two agents (`fix-grammar` and `update-profile`) that silently maintain a per-user language profile at `~/.claude/english-profile.md`.

## Plugin structure

- `.claude-plugin/plugin.json` — plugin metadata (name, version, author)
- `commands/` — slash command definitions (`.md` files with frontmatter + prompt body)
- `agents/` — agent definitions (`.md` files with frontmatter declaring model, tools, color)

## How commands work

Each file in `commands/` is a slash command. The frontmatter `description` field is what appears in the command picker. `$ARGUMENTS` is replaced with whatever the user passes after the command name.

`commands/fix-grammar.md` is a thin prompt — it delegates grammar correction to the `fix-grammar` agent and profile updating to the `update-profile` agent.

## How agents work

Each file in `agents/` defines an agent. The frontmatter declares:
- `model` — which Claude model to use (e.g. `sonnet`)
- `tools` — comma-separated list of tools the agent can call (e.g. `Read, Write`)
- `color` — UI color hint

The agent body is the system prompt. `agents/fix-grammar.md` corrects grammar and outputs the result. `agents/update-profile.md` silently analyzes the original text for error patterns and reads/writes `~/.claude/english-profile.md`.

## Language profile format

`~/.claude/english-profile.md` has a `## Weaknesses` section. Each weakness line ends with a score in parentheses, e.g. `- Missing articles before nouns (3)`. The score increments each time the same mistake is observed. Max 15 entries — when over the limit, the entry with the lowest score is removed.

## Installing / testing locally

```shell
# Load plugin without installing (development)
claude --plugin-dir /path/to/english-claude-plugin

# Or add as a local marketplace and install
/plugin marketplace add /path/to/english-claude-plugin
/plugin install english@english-claude-plugin
```
