@AGENTS.md

## Claude Code

- pstack skills are namespaced as `/pstack:<name>`. They are written with Cursor names, and each one tells you to read the plugin's Claude Code adapter first.
- `.claude/settings.json` is shared: Entire's hooks plus the project plugins (pstack, typescript-lsp). Personal overrides go in `.claude/settings.local.json` (gitignored).
