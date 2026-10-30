# 🏡 Garvey Family Hub

A family super app in one static web page: **calendar + chat + smart home dashboard**, installable on iPhone and Android, hosted free on GitHub Pages.

| Area | What it does |
|---|---|
| 🏠 Home | Today's agenda, reminders, shopping/chores/dinner at a glance, smart home tiles |
| 💬 Chat | Family messages, photos and voice notes (needs Supabase) |
| 📅 Calendar | Work, school, leave, appointments, birthdays; French public holidays and Zone C school holidays 2026-2027 |
| 📋 Lists | Shopping, dinner planner, chores with points |
| ✨ More | Birthdays, appointments, bills and admin, contacts and emergency info, reminders, photos, sync, about |

English and French. Light and dark mode.

## Files
```
index.html              the whole app
manifest.json, sw.js    make it installable and work offline
icon*.png               app icons
supabase/schema.sql     database setup (run once in Supabase SQL Editor)
.github/workflows/      optional GitHub Actions deploy
.github/ISSUE_TEMPLATE/ bug and idea templates
CHANGELOG.md
```

## Deploy
1. Put all files in a GitHub repository.
2. Settings → Pages → Deploy from a branch → `main` / root. (Or choose "GitHub Actions" to use the included workflow.)
3. Open `https://YOUR-USERNAME.github.io/REPO/`, then Add to Home Screen.

## Sync and chat (Supabase)
1. Create a free project at supabase.com.
2. Run `supabase/schema.sql` in the SQL Editor (safe to re-run after updates).
3. In the app: More → Sync → Supabase. Paste Project URL, anon key and a long secret family code (12+ characters). Same code on every phone.

Privacy comes from the secret family code, not user accounts. Do not store passwords in the app.

## Smart home (Home Assistant)
The dashboard starts in demo mode. To control real devices:
1. Run Home Assistant with an **https** address (Nabu Casa, Cloudflare Tunnel or Tailscale).
2. In `configuration.yaml` add your site to CORS:
   ```yaml
   http:
     cors_allowed_origins:
       - https://YOUR-USERNAME.github.io
   ```
3. Create a long-lived access token (Profile → Security).
4. In the app: Home → ⚙️, paste the URL and token. The token stays on that phone only.
5. Home → ✏️ to add tiles using entity IDs such as `light.salon`, `switch.pool_pump`, `sensor.pool_temperature`, `lock.front_door`.

## Development
Edit `index.html`, commit, push. Use Issues for bugs and ideas, and Pull Requests for changes. Version is in `index.html` (`VER`) and `CHANGELOG.md`.

## Modules (Family Hub concept)
| Module | In the app |
|---|---|
| Family | Calendar, birthdays, school, leave, appointments |
| Messaging | Chat with photos and voice (More → Sync → Supabase) |
| Shopping / Tasks | Lists, chores with points, reminders |
| Smart home | Tiles, cameras, alarm, wall display (📺 on Home) |
| House | Maintenance, equipment and warranties, documents (More → House) |
| Money | Shared expenses, monthly budget, bills (More → Money / Bills) |
| Family map | More → Map: each person opts in to share their location on one shared map (Supabase) |
| Quick assistant | Home → Quick add, e.g. "add milk to shopping" (rule-based, not cloud AI) |
| GitHub | This repository: issues, releases, Actions |

## Connecting UniFi, Shelly, Control4, pool and heating
Connect each system to Home Assistant using its built-in integration (UniFi Network / Protect, Shelly, Control4, your pool controller and heating). Then add the entity IDs as tiles. Cameras: add a tile of type Camera with an ID like `camera.front_door`.

## Weather
Uses the free Open-Meteo service. Default location is Lavaur. Change it with `localStorage.setItem('garvey-geo', JSON.stringify({lat:43.7,lon:1.82,n:'Lavaur'}))`.

## Roadmap
Push notifications when the app is closed (server needed), real AI assistant through a server function, Firebase chat, per-person logins, energy charts, meal recipes, shared photo albums.
