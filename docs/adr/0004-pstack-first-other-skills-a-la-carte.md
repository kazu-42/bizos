# pstack first, other skill catalogs à la carte

Coding agents here use pstack (Lauren Tan) as the primary workflow, through the `pstack@cursor-plugins` Claude Code plugin. Only `setup-pstack` is model-invocable; the other 53 skills run only when typed, so the catalog never competes for triggers, and `/pstack:poteto-mode` routes to the rest. (`claude plugin details` still projects about 4.4k always-on tokens for the plugin.) From Matt Pocock's skills we vendor only the grilling cluster (`grilling`, `grill-me`, `grill-with-docs`), `domain-modeling`, `codebase-design`, `writing-for-agents`, and `wizard`. From Addy Osmani's agent-skills we vendor only `security-and-hardening` and `observability-and-instrumentation`, which cover ground pstack does not. Vendored skills are installed with `npx skills` into `.agents/skills/`, symlinked from `.claude/skills/`, and pinned in `skills-lock.json`.

## Considered options

- All three catalogs, whole: rejected. About 110 skills with two routers and three competing TDD and review styles would fight over triggers and fill the context window.
- Addy Osmani's agent-skills as the primary workflow: rejected, because its 25 model-invoked skills and its router would compete with pstack's playbooks.

## Consequences

- Testing and review follow pstack (`/pstack:tdd`, the principle skills, `/pstack:interrogate`, `/pstack:blast-radius`); no second TDD or review skill is vendored.
- Pre-commit tooling must not set `core.hooksPath` (husky does). Entire's hooks live in `.git/hooks` and would silently stop running, which is why Matt's `setup-pre-commit` is excluded.
- pstack is Claude Code only. Codex gets `AGENTS.md` and the vendored skills.
