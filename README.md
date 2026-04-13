# Paceon Landing Page

Static HTML landing page for [paceon.fit](https://paceon.fit), deployed via GitHub Pages.

## Structure

```
paceon-landing/
  index.html      ← Coming-soon page (LIVE now at paceon.fit)
  launch.html     ← Full 11-section landing page (staged for launch day)
  privacy.html    ← Privacy policy (required for App Store)
  terms.html      ← Terms of service
  CNAME           ← paceon.fit (GitHub Pages custom domain)
  .nojekyll       ← Disables Jekyll so HTML is served as-is
  assets/
    screenshots/  ← Drop app screenshots here (see checklist below)
    photos/       ← Lifestyle photos from Unsplash/Pexels
    logos/        ← Wordmarks, integration logos
```

## Local preview

```bash
cd paceon-landing
python -m http.server 8000
# Open http://localhost:8000
```

Preview specific pages:
- http://localhost:8000/index.html — coming-soon (current homepage)
- http://localhost:8000/launch.html — full landing page (to be swapped in at launch)
- http://localhost:8000/privacy.html
- http://localhost:8000/terms.html

Test responsive: in Chrome DevTools, toggle device toolbar (Cmd+Shift+M) and check:
- Mobile: 375px wide (iPhone SE)
- Tablet: 768px
- Desktop: 1280px+

## Deploy

Push to `main` branch. GitHub Pages auto-deploys from root `/` in ~60 seconds.

```bash
git add .
git commit -m "your message"
git push
```

## Before going live: Formspree setup

The email capture on `index.html` uses Formspree. Replace the placeholder with your real endpoint:

1. Sign up at [formspree.io](https://formspree.io) (free)
2. Create a form named "Paceon Launch List"
3. Copy your endpoint URL (e.g. `https://formspree.io/f/xpzgkabc`)
4. In `index.html`, find this line and replace `YOUR_FORM_ID`:
   ```html
   action="https://formspree.io/f/YOUR_FORM_ID"
   ```

## Before going live: DNS configuration

Point `paceon.fit` to GitHub Pages at your domain registrar.

Add these records:

| Type  | Name | Value                    |
|-------|------|--------------------------|
| A     | @    | 185.199.108.153          |
| A     | @    | 185.199.109.153          |
| A     | @    | 185.199.110.153          |
| A     | @    | 185.199.111.153          |
| AAAA  | @    | 2606:50c0:8000::153      |
| AAAA  | @    | 2606:50c0:8001::153      |
| AAAA  | @    | 2606:50c0:8002::153      |
| AAAA  | @    | 2606:50c0:8003::153      |
| CNAME | www  | kjparkdavid.github.io    |

Then in the GitHub repo:
1. Settings → Pages → Source: "Deploy from branch" → `main` → `/` → Save
2. Custom domain: `paceon.fit` → Save
3. Wait for "DNS check successful"
4. Enable "Enforce HTTPS"

## Screenshot checklist (for launch.html)

Capture on iPhone 15 Pro at 3x resolution. Use a demo account with a realistic HM-in-12-weeks plan.
Set status bar to 9:41 AM. Enable light mode.

- [ ] **Hero screenshot** — Today Card (Easy Run, 6km, 5:50/km, coach note)  
      `frontend/app/(app)/dashboard.tsx`
- [ ] **Plan Pulse adapt banner** — "Feeling the load? We reduced next week's mileage"  
      `frontend/app/(app)/dashboard.tsx`
- [ ] **Week plan view** — 7-day pager with day cards and status badges  
      `frontend/app/(app)/plan/index.tsx`
- [ ] **Course card** — map polyline, elevation, PB stat  
      `frontend/app/(app)/courses/[id].tsx`
- [ ] **Workout detail** — pace zone, HR zone, RPE, coach notes  
      `frontend/app/(app)/plan/[id].tsx`

Save screenshots to `assets/screenshots/` and update `<img src>` attributes in `launch.html`.

## Launch day swap

When the app is live and screenshots are in, swap the pages:

```bash
git mv index.html archive-coming-soon.html
git mv launch.html index.html
git commit -m "Launch: promote full landing page"
git push
```

GitHub Pages redeploys in ~60 seconds. The full landing page is live.

## Fonts & colors

Pulled from the app's design system (`frontend/tailwind.config.js`):

| Token       | Value     | Usage                        |
|-------------|-----------|------------------------------|
| bg          | #F7F3EE   | Page background (warm cream) |
| coral       | #C94B2A   | Primary CTA                  |
| forest      | #2A6948   | Success, "completed" states  |
| ink         | #1A1A18   | Body text                    |
| ink-muted   | #6B6B67   | Subtext, labels              |
| cream       | #EDE9E3   | Card backgrounds             |
| Display     | Playfair Display Bold/Italic | Headlines |
| Body        | DM Sans   | All other text               |
