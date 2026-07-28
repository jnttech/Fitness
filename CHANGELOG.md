# Changelog

All notable changes to Phase Tracker, in plain English. Newest first.

## v13 — Per-exercise notes + History "zoom in"
- Added a persistent "My Notes" text box to every exercise's info screen. Notes are keyed by exercise name, so they carry forward and stay in sync everywhere that exercise appears (Day Detail, and any day/week it's scheduled on).
- Clicking an exercise inside a History session now "zooms in" to the same info screen, additionally showing that session's per-set weights (editable) alongside the shared notes.

## v12 — "Today" section + duplicated day workout
- Renamed "Anytime" to "Today."
- Added today's scheduled workout (based on real weekday, Mon=Day1..Sun=Day7) as a duplicate card between Morning Flow and Evening Rolling, so the full day can be done top to bottom in one place. Completion status is shared with the same day's card in "This Week."

## v11 — Export / Import for moving data between devices
- Added a "Backup & Transfer" section (Benchmarks tab) to export your saved data as text, and import it on another device.
- Needed because storage is per-device/per-browser — there's no automatic syncing between your Mac and iPhone.

## v10 — Fixed sizing/tappability on real iPhone hardware
- Fixed buttons being unreachable under the notch and home-indicator bar in standalone (home screen) mode.
- Rebuilt the app's height model to a proper fixed "app shell" (pinned header + tab bar, scrollable middle) using `100dvh`.
- Fixed a layout bug in the guided-workout screen where the bottom controls weren't reliably positioned.

## v9 — iPhone home screen support
- Added Add-to-Home-Screen meta tags and a custom icon (three bars, one per pillar).
- Added a storage fallback: uses Claude's `window.storage` when running as a Claude artifact, or real browser `localStorage` when run standalone.

## v8 — Exercise technique info + weight logging
- Added an "i" button on every exercise row: how to perform it, what to focus on, what to avoid.
- Added optional per-set weight entry during guided workouts.
- Weights preload from the last time you did that exercise, and are visible in exercise history detail.

## v7 — Split Daily Minimum into two items
- "Daily Minimum Flow" became two separate cards: Morning Flow and Evening Rolling, each with its own detail view, sample-idea list, and completion toggle.

## v6 — Set-level Previous/Skip navigation
- Previous/Skip now step through individual sets before moving between exercises, instead of jumping a whole exercise at a time.

## v5 — Rest-timer controls polish
- Rest controls became a fixed-size Pause/Resume (red/green) + Next pair, replacing the old "Skip Rest" button, so labels no longer shift button size.

## v4 — Start Set button + rest-timer bug fix
- Renamed/repositioned the set-completion button to "Start Set" in the middle of the screen.
- Fixed a bug where the final set of an exercise skipped the rest timer and jumped straight to the next exercise.

## v3 — Daily Minimum detail + sample ideas
- Added a dedicated detail view for the Daily Minimum flow with concrete sample movements for morning and evening.

## v2 — Per-day completion toggle
- Added a toggle in the Day Detail view to mark a day complete/not complete, independent of the guided workout flow.

## v1 — Initial app
- Phase 1 plan (Flexibility priority) built as an interactive app: This Week / History / Benchmarks / Roadmap tabs, guided workouts with timers, and persistent progress storage.
