# Fitness Log v2 — Project Documentation

## Overview
A mobile-first, PWA-capable fitness tracking web app for logging workouts, weight, and recovery. Hosted on GitHub Pages with Google Sheets backend for data persistence.

## Live URL
**https://jdelvo06-debug.github.io/fitness-log/**

> Append `?v=N` to bust cache after updates (e.g. `?v=11`)

## Repository
- **GitHub:** `jdelvo06-debug/fitness-log`
- **Branches:** `main` (source) → `gh-pages` (deployed)
- **Local:** `/Users/jeremydelvaux/Projects/fitness-log/`
- **Single file:** `index.html` (all HTML/CSS/JS in one file)
- **PWA:** `manifest.json` (icons: `favicon.png`, `apple-touch-icon.png`, `icon.png`)

## Architecture
- **Frontend:** Static HTML + Tailwind CSS (CDN) + vanilla JavaScript
- **Backend:** Google Sheets via Apps Script Web App API
- **Data storage:** localStorage (primary) + Google Sheets (sync/backup)
- **No build step** — just push `index.html` to `gh-pages` branch

## Google Sheets Integration
- **Sheet ID:** `1jkder4DI5i4mswCMukwZI_KUfAXbnrb0Ghz_PrVsuyI`
- **Apps Script URL:** `https://script.google.com/macros/s/AKfycbx1F4KStHX9MuE2OmzUYs_LQDYkqLkZyjPM3P0zmtsutQxGB-OFJ1uNQZCYQWFaF5pc/exec`
- **Apps Script ID:** `AKfycbx1F4KStHX9MuE2OmzUYs_LQDYkqLkZyjPM3P0zmtsutQxGB-OFJ1uNQZCYQWFaF5pc`
- **Code.gs:** Located in repo root (must be deployed manually to Apps Script)
- **POST requests** use `mode: 'no-cors'` and `Content-Type: application/json`
- **GET requests:** `?action=getWeights` and `?action=getWorkouts`

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
- `appsScriptUrl` — custom Apps Script URL (override)

## Deployment Process
```bash
cd ~/Projects/fitness-log
git add -A
git commit -m "description"
git push origin main
git checkout gh-pages
git merge main
git push origin gh-pages
git checkout main
```

## Known Issues / Future Work
- [ ] Settings modal still shows URL field but URL is hardcoded (cosmetic only)
- [ ] No offline support beyond localStorage (no Service Worker)
- [ ] Dips appears in both triceps and chest exercise lists
- [ ] Recovery tab could show a visual body heatmap
- [ ] Could add progressive overload tracking (trends over time)
- [ ] Could add workout notes per exercise
- [ ] Cardio history not shown in UI (only stored)

## Change History
See [CHANGELOG.md](./CHANGELOG.md)