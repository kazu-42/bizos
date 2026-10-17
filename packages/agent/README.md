# @bizos/agent

The one agent runtime behind every surface: tools, memory, policies, and actions it takes on its own schedule. The bot and the app both call into this package, so they share one memory and one task state ([ADR 0001](../../docs/adr/0001-one-monorepo-with-one-way-dependencies.md)).

- Depends on `@bizos/core` and `@bizos/kb`.
- Knows nothing about Slack or any UI.
- Receives knowledge already filtered by audience ([ADR 0003](../../docs/adr/0003-knowledge-entries-carry-provenance-and-visibility.md)).
