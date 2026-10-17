# app

The super app: knowledge, tasks, task-centered AI communication, and back-office work (attendance, expenses) in one place, with the agent built in.

No framework is chosen yet, so this directory has no package. When it gets one:

- It depends on `@bizos/agent`, `@bizos/kb`, and `@bizos/core`, and never imports the bot.
- Attendance and expenses integrate existing services (for example freee or Money Forward) instead of reimplementing them; legal requirements make those costly to build.
