# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Claude Code plugin that provides English grammar tools. It exposes two slash commands (`/english:fix-grammar` and `/english:english-insights`) and one agent (`fix-grammar`) that silently maintains a per-user language profile at `~/.claude/english-profile.md`.

## Plugin structure

- `.claude-plugin/plugin.json` — plugin metadata (name, version, author)
- `commands/` — slash command definitions (`.md` files with frontmatter + prompt body)
- `agents/` — agent definitions (`.md` files with frontmatter declaring model, tools, color)

## How commands work

Each file in `commands/` is a slash command. The frontmatter `description` field is what appears in the command picker. `$ARGUMENTS` is replaced with whatever the user passes after the command name.

`commands/fix-grammar.md` is a thin prompt — it delegates the actual grammar fix + profile update to `agents/fix-grammar.md` via the skill system.

## How agents work

Each file in `agents/` defines an agent. The frontmatter declares:
- `model` — which Claude model to use (e.g. `sonnet`)
- `tools` — comma-separated list of tools the agent can call (e.g. `Read, Write`)
- `color` — UI color hint

The agent body is the system prompt. `agents/fix-grammar.md` does two things in sequence: outputs corrected text, then silently reads/writes `~/.claude/english-profile.md`.

## Language profile format

`~/.claude/english-profile.md` has three sections: `## Weaknesses`, `## Strengths`, `## Last updated`. One pattern per line, max 15 entries each (oldest removed when over the limit).

## Installing / testing locally

```shell
# Load plugin without installing (development)
claude --plugin-dir /path/to/english-claude-plugin

# Or add as a local marketplace and install
/plugin marketplace add /path/to/english-claude-plugin
/plugin install english@english-claude-plugin
```
