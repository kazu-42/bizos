# bizos

A business OS: a company knowledge base, a Slack bot that works like a colleague, and a super app, built on one shared core. Terms are defined in `GLOSSARY.md`; decisions are in `docs/adr/`.

## Layout

| Path | Package | Role |
| --- | --- | --- |
| `packages/core` | `@bizos/core` | Domain model: people, tasks, knowledge entries, visibility. Pure, no I/O. |
| `packages/agent` | `@bizos/agent` | The one agent runtime behind every surface. No Slack or UI code. |
| `kb` | `@bizos/kb` | Knowledge base: entry schema, ingestion, retrieval. |
| `bot` | `@bizos/bot` | Slack surface; a thin adapter over the agent. |
| `app` | none yet | Super app surface; framework not chosen. |

Dependencies point one way: `bot`/`app` → `agent` → `kb` → `core`, and `bot` and `app` never import each other. A package resolves only the workspace packages its `package.json` declares (an undeclared import fails typecheck with TS2307), so a new edge is a deliberate `package.json` change.

## Invariants

- No company data in the repo: no real knowledge-base content, Slack exports, or secrets. Use synthetic fixtures (ADR 0002).
- Every knowledge entry carries provenance and visibility; retrieval filters by audience before content reaches a model or a channel (ADR 0003).
- Entire records agent sessions in this repo and pushes them with commits. Keep secrets and other organizations' private data out of sessions here.
- Never bypass or relocate git hooks (`--no-verify`, `core.hooksPath`, husky): Entire's hooks live in `.git/hooks`. Never delete or rewrite `entire/*` branches.

## Commands

- `pnpm install`: Node 24 (`.node-version`); pnpm is pinned by `packageManager`.
- `pnpm check`: Biome, then typecheck and tests in every package. Run it before calling work done.
- `pnpm lint:fix`: apply Biome fixes and formatting.
- `pnpm --filter @bizos/<name> <script>`: one package.

TypeScript 7, Biome, Vitest, Turborepo. Packages export TypeScript source (`exports` → `./src/index.ts`); nothing has a build step yet.

## Skills

Rigorous work starts with `/pstack:poteto-mode <task>` in Claude Code: it picks a playbook and pulls in the other pstack skills as its steps need them. Start a Claude worker's Orca prompt with it, too. Otherwise:

| Situation | Skill |
| --- | --- |
| Fuzzy plan or design | `/grill-me`; `/grill-with-docs` also records terms and ADRs |
| Naming a domain concept, recording a decision | `domain-modeling` (`GLOSSARY.md`, `docs/adr/`) |
| Module interfaces and seams | `codebase-design`; types first: `/pstack:architect` |
| What a change could break; adversarial review | `/pstack:blast-radius`; `/pstack:interrogate` |
| Untrusted input, auth, visibility, Slack, webhooks, LLM output, personal data | `security-and-hardening` |
| Code that runs in production | `observability-and-instrumentation` |
| Steps only a human can do (Slack app setup, secrets) | `wizard` |
| Editing `AGENTS.md`, `CLAUDE.md`, or a skill | `writing-for-agents` |

Vendored skills live in `.agents/skills/` (Codex reads them there; `.claude/skills/` symlinks them for Claude Code) and are pinned in `skills-lock.json`. Add one with `npx skills add <owner/repo> --skill <name> --agent claude-code codex`, update with `npx skills update -p`, and don't edit them in place: an update overwrites local changes. pstack and the TypeScript LSP are Claude Code plugins enabled in `.claude/settings.json`. Why this mix: ADR 0004.

## Orca

- Worktrees go in `.worktrees/` (gitignored). Create them with `orca worktree create` (skill `orca-cli`), not raw `git worktree`, so `orca.yaml` installs dependencies before the agent starts.
- `.worktreeinclude` copies `.env.local` into each new worktree.
- Hand off work with `orca-cli`; coordinate several workers with `orchestration`.
