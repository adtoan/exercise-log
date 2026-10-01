# Local-only SQLite for v1, with a sync-ready schema

v1 stores everything in on-device SQLite with no backend, so the app works fully offline and ships without accounts or servers. The schema is shaped so cloud sync (e.g. Supabase) can be added later without migrating identities: UUID primary keys, created/updated timestamps on every row, and soft deletes instead of row removal. Export is JSON with a schema version via the system share sheet; there is no import in v1.

## Considered Options

- Backend from day one: rejected as unnecessary cost and complexity before the core workout flow is proven.
- Auto-increment IDs: rejected because they collide across devices once sync arrives.
