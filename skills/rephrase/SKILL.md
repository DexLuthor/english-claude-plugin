---
description: Rewrite text for clarity and conciseness while preserving meaning
---

Do two things:

1. Use the rephrase agent to rewrite the text below for clarity and conciseness, then show the result to the user.
2. After showing the rephrased text, use the update-profile agent in the background to analyze grammar patterns in the original text and update the language profile.

## Parsing flags

Before obtaining the text, check `$ARGUMENTS` for the following optional flags and strip them from the text:

**Tone flags** (at most one):
- `--formal` — formal tone
- `--casual` — casual tone
- `--concise` — aggressive shortening, remove all filler

If a tone flag is detected, tell the rephrase agent which tone to apply. If no tone flag was provided, do not mention tone to the agent — it will use its default behavior.

## Obtaining text

After stripping any flags, if the remaining text is not empty, use it directly.

If no text remains (i.e. `$ARGUMENTS` is empty/blank or contained only flags), instruct the rephrase agent to read from the system clipboard:
- On macOS: run `pbpaste`
- On Linux: run `xclip -selection clipboard -o`

If the clipboard is also empty or the clipboard command fails, respond with exactly:
"No text found. Either pass text as an argument or copy text to your clipboard first. Usage: `/english:rephrase <text>`"

## Original text

$ARGUMENTS
