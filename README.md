# 💪 Fitness Log v2

Personal workout and weight tracking app with Google Sheets backend.

## Features

- **Workout Tracking**: Log exercises by split (Push/Pull/Upper/Legs)
- **Exercise Swap**: Click "↻ Swap" to choose from ALL exercises for that muscle group + search to filter
- **Weight Logging**: Track weight over time with trend visualization
- **Rest Timer**: Built-in 90s/60s/45s presets
- **Workout History**: View past sessions
- **Muscle Recovery**: Heat map showing recovery status

## Deployment

### Frontend (GitHub Pages)

1. Push this repo to GitHub
2. Go to Settings → Pages
3. Source: Deploy from `main` branch, `/` folder
4. Your site will be live at `https://jdelvo06-debug.github.io/fitness-log/`

### Backend (Google Apps Script)

1. Go to [script.google.com](https://script.google.com/)
2. Create new project
3. Copy `Code.gs` content and paste into the editor
4. Click **Deploy** → **New deployment**
5. Type: **Web app**
6. Execute as: **Me**
7. Who has access: **Anyone**
8. Click **Deploy**
9. Copy the Web App URL
10. In the fitness app, click ⚙️ Settings and paste the URL

## Exercise Database

Includes 60+ exercises across all muscle groups:
- Chest, Back, Shoulders, Triceps, Biceps
- Quads, Hamstrings, Glutes, Calves, Abs

## Tech Stack

- Vanilla JavaScript (no build step)
- Tailwind CSS (via CDN)
- Google Sheets + Apps Script (backend)
- GitHub Pages (hosting)

## License

Personal use
