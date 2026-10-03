# Exercise Log

A mobile workout tracker built around workout efficiency: plan workouts as Templates, run them set by set against a Workout Clock and Rest timers, and keep an accurate record of what was lifted and how long everything took.

## Language

### Planning

**Template**:
A reusable plan for a workout: an ordered list of Exercises, each with its Set Targets. A Workout started from a Template takes its own copy, so later edits to or deletion of the Template never change that Workout.
_Avoid_: Routine, program, plan

**Set Target**:
What one planned set aims for: reps (a single number or a range), weight, RPE and the Rest that follows it. Targets belong to individual sets, so warm-ups and top sets can differ within one exercise.
_Avoid_: Goal, prescription

**RPE**:
Rate of Perceived Exertion, a 1–10 rating of how hard a set felt. Optional when logging.

### Doing

**Workout**:
One occasion of training, started from a Template or empty, recorded as the sets actually performed.
_Avoid_: Session, log, training day

**Workout Clock**:
The overall elapsed time of a Workout, which can be paused and resumed. Pausing it also freezes any Rest in progress.
_Avoid_: Timer, stopwatch

**Active Time**:
A Workout's duration with paused time excluded. The headline duration and the basis for efficiency stats.

**Total Rest Time**:
The sum of every Rest's actual length in a Workout, excluding paused time. Shown on the Workout summary.

**Total Time**:
A Workout's duration from start to finish, including pauses.
_Avoid_: Wall time

**Current Set**:
The set the lifter is performing now, shown with its Set Target and the Workout Clock.

**Logged Set**:
A set that was performed and marked Done, with its actual weight, reps and optional RPE.
_Avoid_: Completed set, entry

**Skipped Set**:
A planned set the lifter chose not to perform. It stays in the record as skipped rather than being deleted. Any set not logged when a Workout finishes becomes a Skipped Set.

**Rest**:
The period between a Logged Set and the moment the lifter chooses to start the next set. Rest does not end on its own; its length, measured from Done to Next set, is the actual rest taken.
_Avoid_: Break, recovery

**Rest Countdown**:
The countdown shown during Rest, starting from the Set Target's rest time and adjustable by ±30 seconds. It stops silently at 0:00 and does not end Rest; +30 seconds at 0:00 starts it counting down again.

**Workout Note**:
Free text attached to a Workout, writable during and after it. There is one per Workout.
_Avoid_: Comment, journal

**Finish Early**:
Ending a Workout before every planned set is done. Logged Sets are kept and the remaining sets become Skipped Sets.

**Discard**:
Removing a Workout from history entirely, after confirmation.
_Avoid_: Abandon, cancel, delete

**Workout Overview**:
The screen listing every set in the current Workout, from which the lifter can jump to, skip, or add sets and exercises. The default order is linear.
