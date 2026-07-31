# Changelog

All notable changes to Phase Tracker, in plain English. Newest first.

## v19 — Cross-device Cloud Sync (opt-in, via Supabase)
- Added a "Cloud Sync" section (Benchmarks tab, above Backup & Transfer) for automatic syncing between devices — no more manual export/import needed for everyday use.
- Fully opt-in: nothing talks to the network unless you generate or enter a sync code. Without one, the app behaves exactly as before (local-only).
- "Generate Sync Code" creates a random code, connects this device, and pushes current data to the cloud. Enter that same code on another device's "Connect" field to link it — the more recently-saved copy wins automatically (simple last-write-wins, since it's one person moving between their own devices, not simultaneous multi-user editing).
- The sync code is the only thing gating access to your data (no separate login system) — treat it like a password, don't share it.
- On the database side: the raw table has no public access at all (RLS enabled, zero policies). Two narrow functions (get/set-by-code) are the only way in or out, each only ever touching the single row matching the code passed in.
- Every local save now also pushes to the cloud in the background (if connected); every app load pulls and reconciles in the background too, without blocking the UI on network access.
- "Disconnect This Device" unlinks local storage from the cloud without deleting anything — reconnecting later with the same code picks the data back up.

## v18 — Automatic week advancement + new benchmark lifts
- Removed the manual "‹ Week ›" navigation. The week display is now derived from a stored phase-start date and today's real date — it advances on its own as calendar weeks pass, and caps at Week 6 of 6.
- Each new week automatically starts with every workout marked not-done again — this falls out naturally from how completion is already tracked per-week, no separate reset step needed.
- If you're upgrading from an older save, your currently-displayed week is preserved rather than jumping when this update lands.
- Benchmarks list replaced: Squat, Deadlift, Bench Press, Row, Overhead Press, Pull-ups, Dips (previously the flexibility-assessment list). Backup & Transfer section is unchanged.

## v17 — Hardened against malformed/malicious data
- Weight values, benchmark entries, and per-set session weights were being inserted into the page as raw HTML strings. A value containing something like `"><script>` could have executed as real code — mainly a risk if you ever imported a backup file from an untrusted source. All of these now go through safe DOM APIs (`textContent`/`.value`) instead, so typed or imported text can never be parsed as markup.
- No functional/visual changes — this is purely a hardening pass.

## v16 — Notes on Morning Flow/Evening Rolling + fuller History detail
- Morning Flow and Evening Rolling's Day Detail screen now has its own "My Notes" box directly visible — no need to tap into the "i" screen first. It shares the same note as everywhere else that exercise appears.
- History session detail now lists every exercise that was part of that session, not just ones with weights entered. Time-based exercises (stretches, cardio, rolling, etc.) show "Tap to view notes" and are still fully clickable through to the shared notes/technique screen.

## v15 — Notes no longer lost on early exit
- Notes only saved to storage when the notes box lost focus. Closing the guided-workout screen or the exercise info screen right after typing (without tapping elsewhere first) could silently drop that note. Both close buttons now force a save first.

## v14 — Notes visible during guided workouts
- The shared per-exercise notes box now also appears at the bottom of the guided workout screen (below the controls and Previous/Skip), editable in place. It reads from and writes to the same shared note as the Day Detail and History views.

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
