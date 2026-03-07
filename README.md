# English Plugin for Claude Code

Tracks your English grammar patterns and fixes grammar on demand — without changing your meaning, tone, or slang.

## Installation

### One-time setup (per machine)

Add this repo as a local marketplace and install the plugin:

```shell
/plugin marketplace add /path/to/english-claude-plugin
/plugin install english@english-claude-plugin
```

Or for development, load it directly without installing:

```shell
claude --plugin-dir /path/to/english-claude-plugin
```

## Commands

### `/english:fix-grammar <text>`

Corrects grammar in the given text. Runs on Haiku for speed. After each correction, silently updates your language profile at `~/.claude/english-profile.md`.

```
/english:fix-grammar i dont know what are you talking about
```

Rules applied:
- Fixes grammatical errors only (tense, agreement, punctuation, articles, etc.)
- Does **not** change meaning, tone, or style
- Does **not** replace or remove slang or colloquialisms

### `/english:english-insights`

Generates a report from your accumulated language profile — weaknesses ranked by frequency, strengths, deeper patterns, and a single focus area recommendation.

```
/english:english-insights
```

> Requires at least a few `/english:fix-grammar` uses to build up the profile.

## Language profile

Your profile is stored at `~/.claude/english-profile.md` and persists across all sessions and projects. You can read or edit it directly at any time.
