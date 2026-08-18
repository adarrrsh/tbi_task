# TBI Task — Countdown Timer

A single-file countdown timer (`index1.html`) with a Start / Reset button.

## Approach

- **Single source of truth for state.** `intervalId` is the only state flag — `null` means stopped, non-null means running. No separate `isStarted` boolean, so the flag can never disagree with whether a timer is actually ticking.
- **Interval handle in module scope.** `intervalId` lives outside `startTimer()` so the click handler can `clearInterval()` a run already in progress. This is what stops repeated clicks from stacking multiple intervals onto the same counter.
- **Single render path.** `render()` reads `timeLeft` and paints `MM:SS`. Initial paint, each tick, and reset all call it, so the formatting logic exists in exactly one place.
- **One duration constant.** `DURATION` (600s) is used for both the initial value and the reset, keeping every run the same length.
- **Self-clearing interval.** The tick decrements, renders, then clears itself the moment it reaches `00:00` — no timer is left running after the countdown ends.
- **Restart from zero.** `startTimer()` refills `timeLeft` if it's already at zero, so a finished timer restarts on a single click.

## Files

- `index1.html` — current version.
- `index2.html` — earlier version, kept for reference.
