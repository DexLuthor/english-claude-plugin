# English Plugin for Claude Code

A Claude Code plugin that improves your written English.
It fixes grammar, adjusts tone, and tracks recurring mistakes so you can polish your language skills over time.

## Installation

Add this repo as a local marketplace and install the plugin:

```shell
/plugin marketplace add https://github.com/DexLuthor/english-claude-plugin
/plugin install english@english-claude-plugin
```

Or for development, load it directly without installing:

```shell
git clone https://github.com/DexLuthor/english-claude-plugin.git
claude --plugin-dir /path/to/english-claude-plugin
```

## Capabilities

### Fixing grammar

#### Running

* Run `/english:fix-grammar [flags] [text]`
* Or ask in plain english: **fix grammar / correct grammar**

> 💡 You can also run without providing text to read from your clipboard

#### Flags

**Tone flags** — adapt corrections to your writing context (at most one):

| Flag       | Behavior                                                     |
|------------|--------------------------------------------------------------|
| `--formal` | Expands contractions, removes slang, enforces full sentences |
| `--casual` | Fixes only clear errors, preserves informal style            |

```
/english:fix-grammar --formal i dont know what are you talking about
```

**Strictness flags** — control how strict corrections are (at most one):

| Flag           | Behavior                                                            |
|----------------|---------------------------------------------------------------------|
| `--strict`     | Only clear grammar errors **(default)**                             |
| `--moderate`   | Grammar fixes plus a Suggestions section for awkward phrasing       |
| `--aggressive` | Grammar fixes plus suggestions for phrasing, conciseness, and style |

```
/english:fix-grammar --moderate i think that maybe we should probably go
```

**File mode** — correct grammar in a file:

```
/english:fix-grammar --file path/to/document.md
```

With `--in-place`, the corrected content is written back to the file (after confirmation):

```
/english:fix-grammar --file path/to/document.md --in-place
```

### Paraphrasing

#### Running

* Run `/english:rephrase [flags] [text]`
* Or ask in plain english: **paraphase/rephrase**

> 💡 Unlike `fix-grammar`, this command actively changes
> wording — not just errors.

#### Flags

**Tone flags** (at most one):

| Flag        | Behavior                                  |
|-------------|-------------------------------------------|
| `--formal`  | Formal tone                               |
| `--casual`  | Casual tone                               |
| `--concise` | Aggressive shortening, removes all filler |

```
/english:rephrase --concise I think that maybe we should probably consider going
```

### Learning from mistakes

Generates a report from your accumulated language profile — mistakes ranked by frequency, deeper patterns, and a
single focus area recommendation.

#### Running

* Run `/english:insights`
* Or ask in plain english: **paraphase/rephrase**

> 💡 Requires at least a few `/english:fix-grammar` uses to build up the profile.

> 💡 `/english:reset-history` Clears your English profile (weaknesses history). Useful if you want to start tracking from
> scratch.

Your profile is stored at `~/.claude/english-profile.md` and persists across all sessions and projects. You can read or
edit it directly at any time.
