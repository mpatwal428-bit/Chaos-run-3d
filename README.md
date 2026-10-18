# CHAOS RUN 3D

Original 3D endless runner. Vite + React + TypeScript + Three.js (React Three Fiber + Drei). No backend, no API keys, no external assets (all geometry is procedural).

## Run locally
```bash
npm install
npm run dev        # http://localhost:5173 (also reachable on your LAN for phone testing)
npm run build      # type-checks and builds to dist/
npm run preview    # serve the production build
```
Requires Node 18+.

## Controls
Keyboard: Arrows/WASD (move, jump, slide), Space (jump), P/Esc (pause), Enter (start). Touch: swipe anywhere or use on-screen buttons.

## Deploy to Vercel
1. Push this folder to a GitHub repo.
2. Go to vercel.com > Add New > Project > import the repo.
3. Framework preset: Vite (auto-detected). Build command `npm run build`, output `dist`.
4. Click Deploy. Every push redeploys. (CLI alternative: `npx vercel` then `npx vercel --prod`.)

## Mobile testing checklist
- [ ] Opens in Chrome on Android, portrait and landscape; no page scroll or pull-to-refresh while playing
- [ ] Swipes in all four directions register; on-screen buttons respond instantly
- [ ] Holds ~50-60 FPS on a mid-range phone; if not, turn on "Reduced effects"
- [ ] Pause works via button, and automatically when switching tabs/apps
- [ ] Sound starts after the first tap; the toggle mutes it
- [ ] Best score persists after reload
- [ ] HUD not hidden by notches/gesture bars
- [ ] Opens on a device with WebGL disabled and shows the friendly error
- [ ] Tutorial hints appear on the first run only (clear site data to retest)

## Monetization
Deploying to Vercel does **not** earn money by itself. Ads pay only after an ad network approves you and serves real ads to real users.

Integration point: `src/ads.tsx` (disabled by default, no publisher IDs, no ad code). Ads can only appear on the menu and game-over screens, never during play.

Readiness checklist:
- [ ] Own a custom domain (most networks, including AdSense, require a site you own; `*.vercel.app` is usually not accepted)
- [ ] Add a privacy policy, contact page, and about/terms page
- [ ] Apply to an ad network (Google AdSense / AdMob-for-web alternatives, or HTML5-game networks such as Google Ad Manager, GameDistribution, CrazyGames, Poki, which have their own SDKs and approval)
- [ ] Wait for publisher approval; only then add your own IDs and code to `adConfig.mount`
- [ ] Add a Consent Management Platform (required for EEA/UK users; implement `hasConsent()`)
- [ ] Follow placement policies: no ads that overlap controls, no accidental-click layouts, no clicking your own ads, no ads that interrupt gameplay, no "click here" encouragement
- [ ] Expect game sites with little content to be rejected by AdSense; portals' SDKs are often an easier route for games

## Limitations / still needs testing
- Dependencies were not installed and `npm run build` was not run in the authoring environment (no network). Run the commands above; fix any version-related type errors if they appear.
- Real-device performance has not been measured; tune `MAXE`, scenery count, and shadows if needed.
- Shapes are primitives (no skeletal animation, particles, or music).
- Difficulty tuning (speed cap 30 m/s, pattern gaps) needs playtesting.
- No leaderboard, gamepad support, or PWA install.
