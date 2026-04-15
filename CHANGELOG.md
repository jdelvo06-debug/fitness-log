# Fitness Log v2 — Changelog

## [2026-04-14] v2.0 — Full Rebuild

### Migration
- Migrated from Here Now (multiple stale deployments) to **GitHub Pages**
- URL: `https://jdelvo06-debug.github.io/fitness-log/`
- Single `index.html` architecture, no build step

### Google Sheets Backend
- Deployed fresh Apps Script project
- POST with `Content-Type: application/json` and `mode: 'no-cors'`
- GET endpoints for weight and workout sync

### Batch 1 — Critical Fixes
- Added `logSet()` function with visual checkmark feedback
- Multiple sets per exercise via "+ Set" button
- Fixed `selectSplit()` — removed fragile global `event` object
- Google Sheets POSTs now have proper headers
- Cardio saves to localStorage + Sheets

### Batch 2 — Major Features
- Rest timer (90s/60s/45s with audio beep via Web Audio API)
- Target weight input + live "To Go" calculation (green/red)
- "+ Add Exercise" button to append any exercise
- "Calf Raise" → "Standing Calf Raise" (exercise DB consistency fix)
- Sync now persists to localStorage (no data loss on reload)

### Batch 3 — Polish & Remaining
- Recovery tab with muscle group grid (color-coded by hours since last trained)
- Delete buttons on weight entries and workout history
- PWA manifest for "Add to Home Screen"

### Smart Exercise Defaults (v2.1)
- Auto-populates sets/reps/weight based on exercise type:
  - Heavy compounds: 4×5
  - Medium compounds: 3×8
  - Isolation: 3×10-12
  - Bodyweight: 3×MAX
- Progressive overload: pulls last workout data, suggests +5lbs if all reps hit
- Muscle group tags on each exercise card
- Set numbers (1, 2, 3...) on each row

### UX Improvements
- Cascade: editing weight/reps fills all non-logged sets in that exercise
- Auto-select on tap — tapping a number field highlights for quick editing
- Numeric keypad on mobile (`inputmode="numeric"`)
- Hidden number spinners via CSS
- Set row layout uses flex-1 for responsive widths
- Mobile-responsive set rows (set numbers hidden on small screens)

### Bug Fixes
- **Critical:** Removed extra closing brace in JS that broke all functionality
- Fixed `Calf Raise` → `Standing Calf Raise` in legs defaults
- `selectExercise()` now rebuilds card with smart defaults (not just text swap)
- `addExercise()` opens swap modal with index -1 for new exercise
- `updateTarget()` and `updateToGo()` now properly calculate weight delta

### Codex CLI
- Codex audit identified 3 bugs (all incorporated above)
- Note: `OPENAI_BASE_URL=http://localhost:11434/v1` in shell env causes Codex to hit Ollama instead of OpenAI. Workaround: `unset OPENAI_BASE_URL` before running `codex`

### Old Deployments (Stale — Do Not Use)
- `velvet-cedar-xtcv.here.now`
- `eager-olive-wcpj.here.now`
- `cobalt-pumice-6stf.here.now`
- `quartz-anvil-kfrs.here.now`