# Knowledge entries carry provenance and visibility

Every knowledge entry records its provenance (where it came from, who wrote it, and when) and its visibility (who may see it), starting with the first schema. Retrieval filters by audience before any content reaches a model or a channel: for a direct message, what the requester may see; for a channel, only what every member may see. The most likely failure of a bot that speaks up on its own is repeating something from a direct message or a private channel in a public one. Access control added later means re-indexing everything, and information that has already leaked cannot be recalled.

## Consequences

- Indexes and embeddings must be filterable by visibility. The agent never receives unfiltered knowledge.
- A response in a channel is limited to what all of its members may see, which can be much narrower than what any single member may see.
