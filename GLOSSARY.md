# bizos

The language of bizos: the company's knowledge, the agent that acts on it, and the surfaces people use to reach both.

## Language

### Knowledge

**Knowledge Base**:
A company's organized, stored context, together with the code that ingests and retrieves it.
_Avoid_: wiki, memory, database

**Knowledge Entry**:
One unit of company knowledge, stored with its provenance and visibility.
_Avoid_: document, record, note

**Provenance**:
Where a knowledge entry came from: its source, its author, and when it was written.
_Avoid_: origin, metadata

**Visibility**:
The set of people allowed to see a knowledge entry.
_Avoid_: permission, ACL, scope

**Audience**:
The people who will see a response: the requester in a direct message, or every member of a channel.
_Avoid_: recipient, viewer

### Agent and surfaces

**Agent**:
The single AI runtime that acts for the company behind every surface.
_Avoid_: assistant, AI, bot

**Surface**:
A place where people reach the agent: the bot or the app.
_Avoid_: client, frontend, channel

**Bot**:
The Slack surface of the agent, which answers and also speaks up on its own.
_Avoid_: Slack app, assistant

**App**:
The super app surface: knowledge, tasks, and back-office work in one place.
_Avoid_: dashboard, portal
