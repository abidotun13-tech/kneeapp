# Knee Check — installing on the Pixel 10a

This is a Progressive Web App. Once installed it behaves like any other app on the
phone: its own icon in the app drawer, full screen with no browser bar, works with
no signal, and keeps its data on the device. It is not on the Play Store, so it
installs from a web address rather than from the store.

## What's in the package

| File | Purpose |
|---|---|
| `index.html` | The whole app — screens, logic, styling |
| `manifest.webmanifest` | Name, icon and colours Android uses when installing |
| `sw.js` | Service worker, so it opens offline |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons (the maskable one is what Android shapes to the launcher) |

All five files must sit in the same folder, and the folder has to be served over
**https** — Android will not offer to install it from a `file://` path or over plain http.

## Option A — Netlify Drop (about two minutes, no account needed to start)

1. On a laptop, go to `app.netlify.com/drop`.
2. Drag the whole unzipped folder onto the page.
3. It returns an address like `https://something-random.netlify.app`.
4. Open that address in **Chrome on the Pixel**.
5. Chrome shows an "Install app" prompt. If it doesn't, use the ⋮ menu → *Add to Home screen* → *Install*.

## Option B — GitHub Pages (better if you want to keep and edit it)

1. Create a repository, upload the five files to the root.
2. Settings → Pages → deploy from `main`, folder `/root`.
3. Open the published address in Chrome on the Pixel and install as above.

## After installing

- The icon lands in the app drawer as **Knee Check**.
- Data is stored on that phone only — nothing is uploaded anywhere, and there is no account.
- Because it stays on the device, it doesn't move to a new phone automatically. The
  **Send my log** button on the Trend screen is the way to get the data out: it opens
  the normal Android share sheet, so it can go to WhatsApp, email, or Google Keep.
- To set a daily reminder, use the Pixel's Clock app: an alarm at wake-up time labelled
  "Score your knees" is more reliable than anything the app could do on its own.

## Updating it later

Re-upload the changed files to the same address. The service worker caches
aggressively, so on the phone: Settings → Apps → Knee Check → Storage → Clear cache,
then reopen. Bumping `CACHE = 'knee-check-v1'` to `v2` inside `sw.js` before
re-uploading does the same job automatically.
