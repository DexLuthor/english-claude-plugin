---
description: Fix grammar without changing meaning, tone, slang, or word choice unless the word itself is grammatically incorrect
---

Do two things:

1. Use the fix-grammar agent to fix grammar in the text below and show the corrected result to the user.
2. After showing the corrected text, use the update-profile agent in the background to analyze grammar patterns in the original text and update the language profile.

## Parsing flags

Before obtaining the text, check `$ARGUMENTS` for the following optional flags and strip them from the text:

**Tone flags** (at most one):
- `--formal` — formal tone
- `--casual` — casual tone

**Strictness flags** (at most one):
- `--strict` — strict mode
- `--moderate` — moderate mode
- `--aggressive` — aggressive mode

**File flags:**
- `--file <path>` — read text from the specified file path (strip both `--file` and the path from arguments)
- `--in-place` — write corrected text back to the file (only valid with `--file`)

## Mode: file

If `--file <path>` is present, operate in **file mode**:

1. Pass the file path to the fix-grammar agent and instruct it to read the file, correct grammar, and output the corrected text with changes.
2. If `--in-place` is also present, tell the agent to write the corrected content back to the file (the agent will ask for confirmation before overwriting).
3. If `--in-place` is used without `--file`, respond with: "The `--in-place` flag requires `--file <path>`. Usage: `/english:fix-grammar --file <path> --in-place`"
4. Tone and strictness flags still apply in file mode.
5. After the fix-grammar agent finishes, use the update-profile agent to analyze the original file content for grammar patterns.

## Mode: inline text

If `--file` is NOT present, operate in **inline text mode** (current default behavior):

After stripping any flags, if the remaining text is not empty, use it directly.

If no text remains (i.e. `$ARGUMENTS` is empty/blank or contained only flags), instruct the fix-grammar agent to read from the system clipboard:
- On macOS: run `pbpaste`
- On Linux: run `xclip -selection clipboard -o`

If the clipboard is also empty or the clipboard command fails, respond with exactly:
"No text found. Either pass text as an argument or copy text to your clipboard first. Usage: `/english:fix-grammar <text>`"

## Tone

If a tone flag was detected, tell the fix-grammar agent which tone to apply:
- `--formal`: Apply formal tone rules
- `--casual`: Apply casual tone rules

If no tone flag was provided, do not mention tone to the agent — it will use its default behavior (fix grammar only, preserve original style).

## Strictness

If a strictness flag was detected, tell the fix-grammar agent which strictness level to apply.

If no strictness flag was provided, do not mention strictness — the agent will fall back to strict mode.

## Output format
Output format must follow the description in [template.md](template.md) 

## Original text

$ARGUMENTS
