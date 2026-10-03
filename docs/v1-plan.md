# Exercise Log: v1 plan

Settled through a one-question-at-a-time design review (2026-10-01 to 2026-10-03). Terms are defined in [CONTEXT.md](../CONTEXT.md); lasting decisions are in [docs/adr](adr/).

## Platform and storage
- React Native with Expo, for iOS and Android. Intended for public release eventually.
- On-device SQLite only, fully offline. The schema is sync-ready: UUIDs, created/updated timestamps, soft deletes ([ADR 0002](adr/0002-local-first-sqlite-sync-ready.md)).
- No export, import or backup in v1. Losing the phone or uninstalling the app loses all data.
- Pounds only. Weights are stored tagged as lb.

## Navigation
- Three bottom tabs: **Templates** (the home screen), **History** and **Exercises** (the Catalog). There is no Settings screen.
- While a Workout is running, a "Resume workout · 23:41" bar sits above the tabs.

## Exercises (Catalog)
- Starts empty. The lifter adds exercises, which have a name only.
- Names that differ only in capitals or spacing count as duplicates and are blocked.
- Renaming updates Templates. Past Workouts keep the old name, and history stays linked.
- Deleting is blocked while a Template uses the exercise, and the message names those Templates. Otherwise the exercise is deleted, past Workouts keep its name, and re-adding the same name creates a fresh exercise.
- Tapping an exercise shows its **Personal Record**: the heaviest weight, with most reps as the tiebreak, derived from history. Skipped Sets don't count.
- See [ADR 0003](adr/0003-workouts-are-snapshots.md).

## Templates
- List → preview (exercises and sets, with **Start** and **Edit**) → editor.
- The editor has one row per exercise: sets, reps (a number or a range), weight, RPE and rest. A row expands so individual sets can vary.
- Required fields: exercise, sets ≥ 1, reps, weight (0 = BW) and rest (prefilled at 2:00). RPE is optional.
- Exercises come from a Catalog picker with an inline "+ Add '…' to catalog" row.
- Exercises can be reordered by dragging. There is no template duplication.
- First launch shows "Create your first template". There is no sample data.

## Running a Workout
- Every Workout starts from a Template. There are no empty workouts, and only one Workout runs at a time (Start becomes Resume).
- The Workout copies the Template when it starts. Template edits never affect it.
- The **Workout Clock** starts on Start and can be paused from any workout screen. A pause freezes Rest too and shows a Paused overlay with Resume.
- Timers are timestamps, not counters ([ADR 0001](adr/0001-timers-as-timestamps.md)).
- The screen stays awake on the workout screens from Start until Finish or Discard. There is no setting.

### Set screen
- Shows the exercise, its Set Target, a "Last: 100 lb × 8" reference (same set, last Workout with this exercise) and the Workout Clock.
- Inputs are weight (number pad plus ±5 lb steppers), reps and RPE.
- Prefill comes from the Set Target: weight, the bottom of a rep range, and RPE if the target has one. Prefilled values appear muted until edited, and they count as filled.
- **Done** is enabled once weight and reps are filled.

### Rest screen
- A **Rest Countdown** from the target's rest time, with ±30s buttons. −30s can't go below 0:00, and +30s at 0:00 counts down again.
- A smaller stopwatch above it shows total rest since Done.
- The countdown stops silently at 0:00. There is no sound, vibration or notification.
- Rest ends only when **Next set** is tapped (or **Finish** after the final set). Next set is available at any time. Actual rest runs from Done to Next set.
- Rest also follows an exercise's last set.

### Workout Overview
- Lists every set. Default order is linear.
- From here the lifter can jump to a set, skip a set, use "+ Set" (copies the exercise's last target) and use "Add exercise" (the one-row editor, rest prefilled 2:00). Additions apply to this Workout only.
- Also holds the Workout Note, **Finish early** (keep logged sets, the rest become Skipped) and **Discard** (confirm, then removed from history).

### Forgotten workouts
- A running Workout resumes when the app reopens.
- If nothing has been logged for over 60 minutes, the app asks "Still working out?" with **Resume** or **Finish at last set** (ends the Workout at the last Logged Set's time).

## Summary (after Finish)
- Shows Active Time, Total Time, Total Rest Time (an experiment), logged and skipped sets, and the Workout Note.
- There is no "Update template?" prompt, and no volume or average-rest stats.

## History
- A list showing the date and Template name, newest first.
- Tapping an entry opens Workout detail. Weight, reps, RPE and the note are editable, and sets can be added or deleted. Times are read-only.

## Explicitly not in v1
Supersets (the data model leaves room for them), kg, export/import/backup, empty workouts, saving a workout as a template, auto-progressing targets, charts, efficiency trends, calendar or streaks, extra exercise fields, merging exercises, duplicating templates, any rest-end alert, a Settings screen.
