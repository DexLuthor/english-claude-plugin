# English Plugin for Claude Code

A Claude Code plugin that provides English grammar tools. It corrects grammar, explains errors, rephrases text, and
tracks your language patterns over time so you can learn from your mistakes.

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

### `/english:fix-grammar [flags] [text]`

Corrects grammar in the given text. After each correction, silently updates your language profile.

```
/english:fix-grammar i dont know what are you talking about
```

**Clipboard mode** — run without text to read from your clipboard:

```
/english:fix-grammar
```

If the clipboard is empty, you'll be prompted to pass text or copy something first.

**Tone flags** — adapt corrections to your writing context (at most one):

| Flag         | Behavior                                                     |
|--------------|--------------------------------------------------------------|
| `--formal`   | Expands contractions, removes slang, enforces full sentences |
| `--casual`   | Fixes only clear errors, preserves informal style            |
| `--business` | Fixes grammar, removes slang, keeps natural contractions     |

```
/english:fix-grammar --formal i dont know what are you talking about
```

**Strictness flags** — control how strict corrections are (at most one):

| Flag           | Behavior                                                            |
|----------------|---------------------------------------------------------------------|
| `--strict`     | Only clear grammar errors (default)                                 |
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

Markdown structure (headings, lists, links) is preserved. Content inside fenced code blocks is not modified. Files over
5000 words produce a warning suggesting to process section by section.

Tone and strictness flags work in file mode too:

```
/english:fix-grammar --file draft.md --formal --moderate
```

### `/english:explain [text]`

Analyzes text and explains every grammar issue with rule names and examples.

```
/english:explain i dont know what are you talking about
```

Each issue includes: the original fragment, the corrected fragment, the grammar rule name, an explanation, and an
additional example. If your language profile has a matching weakness, a profile note is added showing the frequency.

Supports clipboard mode (no arguments) like `fix-grammar`.

### `/english:rephrase [flags] [text]`

Rewrites text for clarity and conciseness while preserving meaning. Unlike `fix-grammar`, this command actively changes
wording — not just errors.

```
/english:rephrase I think that maybe we should probably consider going to the store
```

**Tone flags** (at most one):

| Flag        | Behavior                                  |
|-------------|-------------------------------------------|
| `--formal`  | Formal tone                               |
| `--casual`  | Casual tone                               |
| `--concise` | Aggressive shortening, removes all filler |

```
/english:rephrase --concise I think that maybe we should probably consider going
```

Supports clipboard mode (no arguments) like `fix-grammar`.

### `/english:insights`

Generates a report from your accumulated language profile — weaknesses ranked by frequency, deeper patterns, and a
single focus area recommendation.

```
/english:insights
```

> Requires at least a few `/english:fix-grammar` uses to build up the profile.

### `/english:reset-history`

Clears your English profile (weaknesses history). Useful if you want to start tracking from scratch.

```
/english:reset-history
```

Your profile is stored at `~/.claude/english-profile.md` and persists across all sessions and projects. You can read or
edit it directly at any time.

The profile tracks:

- **Weaknesses** — each entry has a score showing how many times the pattern was observed (e.g.,
  `Missing articles before nouns (3)`)
- Maximum 15 entries — when over the limit, the least frequent entry is removed
- Scores increment each time the same mistake is detected

All commands that process text (`fix-grammar`, `explain`, `rephrase`) update the profile automatically.
