# Company data stays out of the repo

Knowledge base content, Slack history, documents, and secrets never live in this repository. If they did, access to the code would grant access to everything the company knows, git history would keep it forever, and the bot's continuous writes would bury the code history. `kb/` holds the schema, ingestion, and retrieval code; the content lives in a separate private store with its own access control (a private repository or a database, not chosen yet). Tests and examples use synthetic data.
