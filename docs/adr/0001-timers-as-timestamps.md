# Timers are stored as timestamps, not ticking counters

The Workout Clock and Rest are persisted as start/pause/end timestamps and derived on display, rather than counters incremented every second. Mobile OSes suspend backgrounded apps, so a ticking counter drifts or stops; timestamps stay exact, survive app restarts, and let a scheduled local notification fire when Rest ends even while the app is suspended. Timer accuracy is the core feature of the app, so this is non-negotiable.
