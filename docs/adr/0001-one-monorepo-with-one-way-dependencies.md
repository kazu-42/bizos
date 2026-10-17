# One monorepo, dependencies point one way

bizos lives in one pnpm and Turborepo monorepo: `packages/core`, `packages/agent`, `kb`, `bot`, and `app`. Early on, the domain model (people, tasks, knowledge, visibility) changes across every part at once, so one pull request should be able to change them together, and coding agents should see the whole system. Dependencies point one way, `bot`/`app` → `agent` → `kb` → `core`, and the bot and the app never import each other. The agent runtime is its own package so that the bot and the app share one memory and one task state instead of growing two diverging AIs.

## Considered options

- One repository per part: rejected while the domain model is still moving, because every cross-cutting change would need coordinated releases across repositories.

## Consequences

- A package resolves only the workspace packages its `package.json` declares; pnpm's strict `node_modules` makes an undeclared import fail typecheck. Adding a dependency edge is therefore a visible `package.json` change.
- Company data is the exception and stays out of this repository (ADR 0002).
