---
description: Generate a report analyzing your English language patterns and weaknesses
disable-model-invocation: false
---

Read the file at `~/.claude/english-profile.md`.

If the file does not exist or is empty, respond with:
"No English profile found yet. Use `/english:fix-grammar` a few times to build up your profile."

Otherwise, generate a structured insights report with the following sections:

---

## English Language Insights

### Current Weaknesses
Each weakness in the profile has a score in parentheses (e.g. `(5)`) showing how many times it was observed. Present them as a **markdown table** ranked by score from highest to lowest, with these exact columns:

| # | Weakness | Score | Why it's common |
|---|----------|-------|-----------------|

Number rows sequentially starting from 1. The "Why it's common" column should contain a brief one-line explanation.

### Summary
Interpret the scores briefly. Call out the most persistent issue (highest score) by name and count — e.g., "You've made [weakness] [N] times — this is your most persistent pattern." If several weaknesses share high scores, mention the cluster.

### Focus Area
Recommend the single most impactful grammar topic to work on next. Use **both** frequency (score) and foundational importance to decide: high-score weaknesses should be prioritized because they represent the most persistent patterns, but between equally frequent issues, prefer the one with broader impact on clarity. Include one practical tip.

### Typing habits
Identify any typing habits — e.g., not capitalized "I", missing period at the end of sentences. Keep this section concise: 2–4 observations. Each observation must start with a **bold keyword** followed by an em-dash and explanation. Example format:

- **Capitalization** — you consistently write "i" instead of "I"
- **Punctuation** — sentences often end without a period

---

Keep the tone direct and practical, like a language coach giving a quick debrief. No filler.

When giving examples throughout the report, wrap them in inline code spans (backticks). For instance: contractions like `"Im"` instead of `"I'm"`.
