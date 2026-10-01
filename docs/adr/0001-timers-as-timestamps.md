# Timers are stored as timestamps, not ticking counters

The Workout Clock and Rest are persisted as start/pause/end timestamps and derived on display, rather than counters incremented every second. Mobile OSes suspend backgrounded apps, so a ticking counter drifts or stops; timestamps stay exact and survive app restarts. Timer accuracy is the core feature of the app, so this is non-negotiable.

The Rest Countdown reaching 0:00 deliberately gives no signal (no sound, vibration or notification): with 2–4 minute rests, frequent alerts were judged too intrusive. Rest only ends when the lifter taps Next set, and the time up to that tap is recorded as the actual rest.
