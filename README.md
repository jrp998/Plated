# Plated — installable app package

This folder is a complete Progressive Web App. Once served over HTTPS, both phones can install it to the home screen and run it fully offline — own icon, no browser bar.

## Folder contents
```
index.html          the app (this is your plated.html, renamed + PWA-wired)
manifest.json       app name, icons, standalone display
sw.js               service worker — caches everything for offline use
icons/              app icons at every size the OS asks for
```
Keep this structure intact. `index.html`, `manifest.json` and `sw.js` must sit in the **same folder**, with `icons/` beside them.

## Why it needs hosting
Service workers (the offline magic) only run over **https://**, never from a `file://` opened directly. You need to serve the folder from somewhere with HTTPS. All the options below are free and take a few minutes.

---

## Option A — GitHub Pages (recommended)
1. Create a new repo (e.g. `plated`), public or private both work.
2. Upload the entire contents of this folder to the repo root (drag-and-drop in the GitHub web UI is fine).
3. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**, pick `main` / root, Save.
4. Wait ~1 min. Your URL appears: `https://<your-username>.github.io/plated/`
5. Open that URL on each phone → install (see below).

Updating later: replace `index.html` in the repo, and bump `CACHE = 'plated-v1'` to `'plated-v2'` in `sw.js` so phones pull the new version instead of the cached one.

## Option B — Netlify Drop (fastest, no git)
1. Go to https://app.netlify.com/drop
2. Drag this whole folder onto the page.
3. You get an instant HTTPS URL. Done. (Free account lets you keep/rename it.)

## Option C — Cloudflare Pages
Similar to GitHub Pages; connect a repo or direct-upload. Also free, very fast globally.

---

## Installing on the phone (after you have the URL)

**Android / Chrome:** open the URL → menu (⋮) → **Add to Home screen** / **Install app** → it lands in your app drawer with the Plated icon and launches with no browser chrome.

**iPhone / Safari:** open the URL → Share button → **Add to Home Screen**.

First load caches everything; after that it opens offline. Your grocery list, hidden meals and week plan are stored per-device.

---

## Later: a real Play Store APK
When you want an installable `.apk` (or a Play listing), this same folder feeds straight into:
- **Bubblewrap** (`npx @bubblewrap/cli init --manifest https://<your-url>/manifest.json`) → signed APK from the live PWA, or
- **Capacitor** if you'd rather bundle the files directly into an Android Studio project.

Nothing here is throwaway — the PWA is the foundation both tools build on.
