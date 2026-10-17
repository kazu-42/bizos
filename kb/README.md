# @bizos/kb

The knowledge base: the knowledge entry schema, ingestion from sources, indexing, and retrieval.

- Code only. Company content lives in a separate private store, never in this repo ([ADR 0002](../docs/adr/0002-company-data-stays-out-of-the-repo.md)). Tests use synthetic data.
- Every entry records provenance and visibility, and retrieval filters by audience ([ADR 0003](../docs/adr/0003-knowledge-entries-carry-provenance-and-visibility.md)).
- Depends on `@bizos/core`.
