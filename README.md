# bizos

A business OS in three parts on one shared core:

- **Knowledge base** (`kb/`): organizes and stores the company's context.
- **Bot** (`bot/`): an always-on Slack member that works like a colleague, from concierge requests to manager-style task follow-up.
- **App** (`app/`): a super app with knowledge, tasks, task-centered AI communication, and back-office work (attendance, expenses) in one place.

The knowledge base is the foundation. The bot and the app are two surfaces over the same agent (`packages/agent`) and domain model (`packages/core`); see [ADR 0001](docs/adr/0001-one-monorepo-with-one-way-dependencies.md).

## Getting started

Requires Node 24 (`.node-version`) and pnpm (pinned by `packageManager`; run `corepack enable` if pnpm is missing).

```sh
pnpm install
pnpm check   # Biome, typecheck, tests
```

## Working with coding agents

[`AGENTS.md`](AGENTS.md) is the source of truth for agents; `CLAUDE.md` imports it.

- **Claude Code** loads the pstack and TypeScript LSP plugins from `.claude/settings.json` (accept the install prompt the first time you trust the folder). Start rigorous work with `/pstack:poteto-mode`, and stress-test a fuzzy plan with `/grill-me`.
- **Codex** reads `AGENTS.md` and the vendored skills in `.agents/skills/`.
- **Orca** creates worktrees under `.worktrees/` and runs `pnpm install` in each one (`orca.yaml`).
- **Entire** links agent sessions to commits as checkpoints.

## Decisions and language

- [`docs/adr/`](docs/adr/): architecture decisions.
- [`GLOSSARY.md`](GLOSSARY.md): domain terms.
