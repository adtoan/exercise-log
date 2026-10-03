# Workouts are snapshots; Templates and the Catalog are live

A Workout copies its Template's sets and targets when it starts, and records each Exercise's name as it was at the time. Templates point to Catalog Exercises live, so a rename shows up in Templates straight away, but editing or deleting a Template or an Exercise never changes a Workout that already happened. History stays linked to its Exercise through renames (for "Last:" references and future stats). Deleting an Exercise that a Template still uses is blocked. Re-adding a deleted name creates a fresh Exercise with no history.

## Considered Options

- Fully live references (workouts show current names): rejected because past records should read exactly as they were logged.
- Free-text names with no Catalog: rejected because typos would split history and a later Catalog migration would be painful.
