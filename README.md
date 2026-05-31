# Active Life

A gamified bodyweight-training PWA — Duolingo-style mechanics, Jujutsu Kaisen theme.
Single-file React app (in-browser Babel), no build step, hosted free on GitHub Pages.

See `DESIGN.md` for the full concept, the trainer's input, and the design rationale.

## Files
- `index.html` — the whole app (React via CDN, all state in `localStorage`)
- `manifest.webmanifest` — PWA manifest
- `sw.js` — service worker (offline support)
- `icon.svg` — app icon

## Run locally
Because of the service worker, open it via a tiny local server (not `file://`):

```bash
cd active-life
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploy to GitHub Pages
1. Create a repo under your account (`vcanela`), e.g. `active-life`.
2. Push these files to the `main` branch (root, not a subfolder).
   ```bash
   git init && git add . && git commit -m "Active Life v1"
   git branch -M main
   git remote add origin https://github.com/vcanela/active-life.git
   git push -u origin main
   ```
3. Repo → **Settings → Pages** → Source: `main` / `/ (root)` → Save.
4. Open `https://vcanela.github.io/active-life/`.
5. On your phone: open that URL → **Add to Home Screen** → launches as a standalone app.

## Notes / next steps
- All exercise data lives in the `GROUPS`, `FLEX_LADDER`, `CHARACTERS` arrays near the top of
  the `<script type="text/babel">` block — easy to tweak.
- Production polish later: precompile JSX (drop in-browser Babel for speed), real PNG icons for
  crisper iOS install, optional "freeze" mechanic, per-area test logging with RoM history.
