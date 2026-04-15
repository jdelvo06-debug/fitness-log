# 💪 Fitness Log v2

Personal workout and weight tracking app with Google Sheets backend.

**🔗 Live App:** [jdelvo06-debug.github.io/fitness-log](https://jdelvo06-debug.github.io/fitness-log/)

## Features

- **Smart Exercise Defaults** — Auto-populates sets/reps/weight by exercise type (heavy compounds 4×5, medium 3×8, isolation 3×10, bodyweight 3×MAX)
- **Progressive Overload** — Suggests +5lbs when all target reps were hit last session
- **Cascade Input** — Edit weight/reps on one set, it fills the rest
- **Numeric Keypad** — Mobile-friendly numpad + auto-select on tap
- **Workout Tracking** — Log exercises by split (Push/Pull/Upper/Legs)
- **Exercise Swap** — Click "↻ Swap" to choose from all exercises for that muscle group with search
- **Weight Logging** — Track weight over time with target and trend display
- **Rest Timer** — Built-in 90s/60s/45s presets with audio beep
- **Workout History** — View past sessions with delete support
- **Muscle Recovery** — Color-coded grid showing recovery status by muscle group
- **Cardio Warmup** — Log warmup jog/run/bike with distance and time
- **PWA** — Add to Home Screen for app-like experience

## Architecture

- **Frontend:** Single `index.html` (HTML + Tailwind CSS + vanilla JS)
- **Backend:** Google Sheets via Apps Script Web App API
- **Hosting:** GitHub Pages (gh-pages branch)
- **Data:** localStorage (primary) + Google Sheets (sync/backup)

## Deployment

### Frontend (GitHub Pages)

Pushed automatically via `gh-pages` branch — any merge to `main` should be merged into `gh-pages` and pushed.

```bash
git checkout gh-pages && git merge main && git push origin gh-pages && git checkout main
```

### Backend (Google Apps Script)

1. Open [Apps Script](https://script.google.com)
2. Copy `Code.gs` into the editor
3. Deploy → New deployment → Web app → Execute as Me → Anyone
4. Update `APPS_SCRIPT_URL` in `index.html` if the URL changes

## Documentation

- [PROJECT.md](./PROJECT.md) — Full architecture, features, and deployment details
- [CHANGELOG.md](./CHANGELOG.md) — Version history and bug fixes