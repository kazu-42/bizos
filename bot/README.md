# @bizos/bot

The Slack surface. It receives Slack events, hands them to `@bizos/agent`, and posts what the agent returns, including messages the agent decides to send on its own.

- A thin adapter: business logic belongs in `@bizos/agent` or `@bizos/core`.
- Depends on `@bizos/agent` and `@bizos/core`. Never imports the app.
- Slack credentials come from `.env.local` (gitignored, copied into Orca worktrees by `.worktreeinclude`).
