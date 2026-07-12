# Morning Protocol

A single-file, offline, rule-based PWA for morning readiness. Enter 6–8 data
points from a Garmin Venu 4 plus subjective inputs; get a GREEN/YELLOW/RED
verdict, the day's adjusted workout, nap guidance, a bedtime target, and a
step goal. Sundays generate a weekly review. No AI, no network calls, all
data in localStorage.

## Files

- `index.html` — the entire app (all CSS and JavaScript inline)
- `manifest.webmanifest` — web app manifest for standalone/home-screen launch
- `sw.js` — small service worker so the app opens offline
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — icons

## Deploy to Netlify

Option A — drag and drop (fastest):
1. Go to https://app.netlify.com/drop
2. Drag the repository folder (or a folder containing the six files above) onto the page.
3. Netlify gives you a `https://<name>.netlify.app` URL. Optionally rename it under Site settings → Domain management.

Option B — from this Git repo:
1. Netlify dashboard → Add new site → Import an existing project → connect GitHub → pick this repo.
2. Build command: none. Publish directory: `/` (repo root).
3. Deploy. Every push redeploys automatically.

HTTPS is automatic on Netlify, which is required for the service worker.

## Add to iPhone home screen

1. Open the Netlify URL in **Safari** (must be Safari, not Chrome or an in-app browser).
2. Tap the **Share** button (square with arrow).
3. Scroll down, tap **Add to Home Screen**, then **Add**.
4. Launch from the home-screen icon. It opens full-screen with no browser chrome.

Data note: localStorage in the home-screen app is separate from Safari's and is
device-specific. Use Settings → Export JSON weekly; the app nags after 7 days.

## Export format

Exports are a flat JSON object with an `entries` array of dated objects
(`date`, `checkin`, `verdict`, `reason`, `evening`, `measurements`), plus
`settings` and `meta` — ready to load into a hosted database later without
transformation.
