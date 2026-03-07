# Privacy Policy

**English Plugin for Claude Code**

Last updated: 2026-03-07

## Data collection

This plugin does **not** collect, transmit, or store any personal data on external servers.

## Local data storage

The plugin stores a language profile at `~/.claude/english-profile.md` on your local machine. This file contains:

- A list of grammar weakness patterns (e.g., "Missing articles before nouns")
- Frequency scores for each pattern

This data never leaves your machine. It is not sent to any server, analytics service, or third party.

## How to delete your data

Run `/english:reset-history` to clear your profile, or simply delete the file:

```shell
rm ~/.claude/english-profile.md
```

## Third-party services

This plugin does not integrate with or send data to any third-party services. All text processing is performed by the Claude model that is already running in your Claude Code session.

## Contact

If you have questions about this policy, open an issue at https://github.com/DexLuthor/english-claude-plugin/issues.
