# Fitness Log — Project Documentation

## Overview
A mobile-first, PWA-capable fitness tracking web app for logging workouts, weight, and recovery. Hosted on GitHub Pages with Supabase cloud backend for data persistence and sync.

## Live URL
**https://jdelvo06-debug.github.io/fitness-log/**

## Repository
- **GitHub:** `jdelvo06-debug/fitness-log`
- **Branch:** `gh-pages` (deployed directly — no separate source branch)
- **Single file:** `index.html` (all HTML/CSS/JS in one file)
- **PWA:** `manifest.json` (icons: `favicon.png`, `apple-touch-icon.png`, `icon.png`)

## Architecture
- **Frontend:** Static HTML + Tailwind CSS (CDN) + vanilla JavaScript
- **Backend:** [Supabase](https://supabase.com) (PostgreSQL, REST API via `@supabase/supabase-js@2`)
- **Data storage:** localStorage (primary) + Supabase (cloud sync/backup)
- **No build step** — just push `index.html` to `gh-pages` branch

## Supabase Integration
- **Project URL:** `https://gnxreojfvrzmgpmjxaql.supabase.co`
- **Credentials:** Hardcoded in `index.html` (`SUPABASE_URL` / `SUPABASE_KEY`). Overridable via Settings modal, persisted to localStorage.
- **CDN:** `https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2` (UMD build, exposes `window.supabase`)
- **Client variable:** `supabaseClient` in inline script (distinct from `window.supabase` CDN global)

### Tables
| Table | Columns |
|---|---|
| `weights` | `id`, `date`, `weight` |
| `workouts` | `id`, `date`, `split`, `duration` |
| `exercises` | `id`, `workout_id`, `name`, `sets` (JSON) |
| `cardio` | `id`, `date`, `type`, `distance`, `duration` |

### Key Functions
- `logWeight()` → upsert into `weights`
- `logCardio()` → insert into `cardio`
- `endWorkout()` → insert into `workouts` + `exercises`
- `syncData()` → read from all tables, merge with localStorage

## Features (Current)
### Workout Tab
- 4 splits: Push, Pull, Upper, Legs
- **Smart exercise defaults** — auto-populates sets/reps/weight by exercise type:
  - Heavy compounds (Bench, Squat, Deadlift, OHP): 4×5
  - Medium compounds (Leg Press, Rows, Lunges): 3×8
  - Isolation (Curls, Flyes, Raises): 3×10
  - Bodyweight (Pull-ups, Dips, Push-ups): 3×MAX
- **Progressive overload** — pulls last workout data; if all reps hit, suggests +5lbs
- **Cascade** — editing weight/reps fills all non-logged sets in that exercise
- **Auto-select on tap** — tapping a number field highlights it for quick editing
- **Numeric keypad** — `inputmode="numeric"` on all number fields
- **Set numbers** (1, 2, 3...) on each row
- **Muscle group tags** on each exercise (Chest, Tri, Bi, etc.)
- **Exercise swap** — modal with search across all exercises for the split
- **+ Add Exercise** — append any exercise to current workout
- **Log Set** — marks set complete, disables inputs, adds next set row
- **+ Set** — adds another set row pre-filled with previous values
- **Rest timer** — 90s/60s/45s with audio beep
- **Workout timer** — start/end with elapsed time display
- **Cardio warmup** — type, distance, time logging

### Weight Tab
- Current / Target / To Go display
- Target weight input (persists to localStorage)
- Color-coded "To Go" (green = at/below target, red = above)
- Weight log with delta comparison to previous entry
- Delete weight entries (✕ button)
- Sync to/from Google Sheets

### History Tab
- Last 10 workouts with date, split, duration, exercises/sets
- Delete workout entries (✕ button)

### Recovery Tab
- Muscle group recovery grid (10 groups)
- Color-coded: 🟢 Ready (72h+), 🟡 Almost (48-72h), 🔴 Rest (<48h), gray = no data
- Updates after logging workouts or syncing

### Settings
- Apps Script URL config (currently hardcoded)

## Exercise Database
- 10 muscle groups: chest, back, shoulders, triceps, biceps, quads, hamstrings, glutes, calves, abs
- 80+ exercises total
- Default workouts per split:
  - **Push:** Bench Press, Incline DB Press, Cable Fly, OHP, Lateral Raises, Tricep Pushdown, Cable Crunch
  - **Pull:** Pull-ups, Lat Pulldown, Barbell Row, Seated Row, Face Pulls, Barbell Curl, Hammer Curl
  - **Upper:** Bench Press, Pull-ups, OHP, Barbell Row, Lateral Raises, Tricep Pushdown, Barbell Curl
  - **Legs:** Squat, Leg Press, Romanian Deadlift, Leg Extension, Leg Curl, Standing Calf Raise, Cable Crunch

## localStorage Keys
- `fitnessLogWeights` — weight entries array
- `fitnessLogHistory` — workout history array
- `fitnessLogCardio` — cardio entries array
- `fitnessLogTargetWeight` — target weight number
- `supabaseUrl` — custom Supabase project URL (override)
- `supabaseKey` — custom Supabase anon/publishable key (override)

## Deployment Process
```bash
cd ~/projects/fitness-log
git add -A
git commit -m "description"
git push origin gh-pages
```

> The `gh-pages` branch is the live deployment branch. Push directly to it.

## Known Issues / Future Work
- [ ] No offline support beyond localStorage (no Service Worker)
- [ ] Dips appears in both triceps and chest exercise lists
- [ ] Recovery tab could show a visual body heatmap
- [ ] Could add progressive overload tracking (trends over time)
- [ ] Could add workout notes per exercise
- [ ] Cardio history not shown in UI (only stored)
- [ ] `Code.gs` in repo root is legacy (Google Sheets era) — no longer used

## Change History
See [CHANGELOG.md](./CHANGELOG.md)