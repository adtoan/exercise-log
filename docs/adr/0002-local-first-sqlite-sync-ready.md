# Local-only SQLite for v1, with a sync-ready schema

v1 stores everything in on-device SQLite with no backend, so the app works fully offline and ships without accounts or servers. The schema is shaped so cloud sync (e.g. Supabase) can be added later without migrating identities: UUID primary keys, created/updated timestamps on every row, and soft deletes instead of row removal. Weights are stored with an explicit unit (always lb in v1) so kg can be added without a migration.

v1 has no export, import or backup. Uninstalling the app or losing the phone loses all data; this is an accepted v1 risk.

## Considered Options

- Backend from day one: rejected as unnecessary cost and complexity before the core workout flow is proven.
- Auto-increment IDs: rejected because they collide across devices once sync arrives.
- JSON export via the share sheet: planned, then cut from v1 to reduce scope.
