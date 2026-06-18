# FMX 2026 — Kitsu booth slideshow

Single-file HTML slideshow that loops on the booth screen at FMX (Stuttgart, May 5-7, 2026). CGWire shows it between live demos of Kitsu (open-source production tracking for animation and VFX studios).

## Files

- `index.html` — the whole slideshow. CSS and JS are inline. No build, no framework, no npm.
- `assets/` — image assets referenced by the slideshow. Most are placeholders to be replaced.
- `design/` — reference design source (`slideshow-calm.html` + assets). Not shipped, not loaded by `index.html`. Treat as a frozen reference; live changes go in `index.html`.
- `fmx-2025.pdf` — last year's deck, used as visual reference. Do not ship.

## How it runs

Open `index.html` in Chrome or Firefox. Press `F` for fullscreen.

- Auto-advances every 10 seconds, loops forever
- 600ms crossfade between slides
- Persistent chrome at the top: Kitsu badge + `FMX 2026 · Stuttgart · Booth 1.4`
- Bottom footer: thin green progress bar, `01 / 13` counter, dot indicators, "Auto-advance · 10s" label
- Keyboard: `F` fullscreen, `Space` pause, `←` / `→` (or PageUp/PageDown) navigate, `Home` restart

## Slide order (13 slides)

Each content slide has an **eyebrow** (small uppercase green label) above an **h1** with one accented phrase wrapped in `<em>` (rendered green, not italic).

1. Logo — Kitsu mark + wordmark + green divider + tagline "Production Tracking · Animation & VFX"
2. "The Reality Today" / "Productions are getting more complex" — 2x2 grid with icon + label + sub (Tighter budgets / Shorter deadlines / Remote teams / Multi-studio projects)
3. "An unified workspace" — UI screenshot (with detailed mock-UI fallback behind)
4. "Built-in review" / "Powered by a review engine" — review-engine screenshot (with simple play-icon fallback behind)
5. "Smart scheduling" / "Plan and reschedule, at a glance" — schedule screenshot (with simple calendar-icon fallback behind)
6. "What we bring" / "Everything your studio needs, connected" — 3 feature cards with icon, title, description, tag pills (Review / Track / Connect)
7. "Built for everyone" / "One tool, every role" — hexagon with 6 stakeholders (Production / Supervisors / Directors / Clients / Accounting / Artists) around the Kitsu mark
8. "Multi-studio, by design" / "One backbone, many studios" — 3 hexagons (Studio One / Studio Two / Producer) meeting at the Kitsu mark, plus one-line caption
9. "By the numbers" / "Trusted at every scale" — 3 stats: 400+ studios worldwide / 30 countries / 20k+ daily artists
10. "Working studios" / "Studios that ship with Kitsu" — 4x3 logo grid
11. "Selected productions" / "Recent shows, tracked in Kitsu" — 4 posters in a row
12. "2026 release" / "What's new in Kitsu" — 3 news cards with NEW pill (Budget Management / Smart scheduling / Playlist 2.0)
13. Contact — "Come Talk To Us" + "See Kitsu live, at the booth." + kitsu.cg-wire.com + green Booth 1.4 badge + QR

## Visual conventions

Authentic Kitsu / CGWire palette (don't substitute approximations):

- Background `#25282E` (k-dark-grey), elevated `#2D2E36`, soft `#36393F`, deep `#202225`
- Accent green `#00B242`, light `#7AE3A0`, dark `#008732`
- Text white `#FEFEFE`, muted `rgba(255,255,255,0.62)`, faint `rgba(255,255,255,0.38)`
- Borders `rgba(255,255,255,0.08)` / `0.16`
- Font: Lato (Google Fonts), weights 300/400/700/900. Black (900) for h1/h2/wordmark/numbers, 700 for eyebrows/labels, 400 for body.
- Subtle radial vignette over the stage
- Large, centered text, lots of whitespace
- No bullet points
- No em dashes (use commas or periods)
- Never mention competitors (Flow, ftrack, AYON, ShotGrid)
- "Open source" can appear but is not central in this booth context
- Tone: factual and confident, not aggressive

## Asset placeholder pattern

Each image asset has a styled visual fallback rendered behind it. The `<img>` covers the fallback when it loads; `onerror="this.remove()"` strips the broken `<img>` so the fallback shows through. Drop the file at the expected path and it just appears, no HTML edit needed.

```html
<div class="poster" style="--ph-a:#3a4a5e;--ph-b:#0f1218">
  <div class="placeholder">…rich styled fallback (badge, silhouette, title, subtitle)…</div>
  <img src="./assets/poster-01.jpg" alt="" onerror="this.remove()">
</div>
```

The fallbacks are rich (mock UI for the screenshot, mono+name tile for logos, gradient+silhouette+title for posters, fake QR grid with the Kitsu mark in the center) — the slideshow looks intentional even with no assets at all.

## Assets expected in `./assets/`

- `kitsu-mark-styled.svg` — already present, used on slides 1 and 13. Authoritative copy lives in `design/assets/`.
- `screenshot-ui.png` — Kitsu interface screenshot (16:10 ideal, covers the mock UI on slide 3)
- `review.png` — Kitsu review-engine screenshot (covers the play-icon fallback on slide 4)
- `schedule.png` — Kitsu scheduling-view screenshot (covers the calendar-icon fallback on slide 5)
- `logo-client-01.png` … `logo-client-12.png` — client studio logos (any aspect, inverted to white via CSS filter)
- `poster-01.jpg` … `poster-04.jpg` — film/series posters (portrait, 2:3 ideal)
- `qr-code.png` — QR pointing to kitsu.cg-wire.com or a cloud trial form

## SVG diagrams (slides 7 & 8)

Both diagrams are SVG inline, no asset needed. The hexagons are written with raw point coordinates; if you need to resize or reposition labels, edit the `viewBox` and `<text>` x/y directly.

The Kitsu wolf mark is duplicated as inline SVG paths in the chrome and slides 7, 8, and the QR center on slide 13. Slides 1 and 13 use `<img src="./assets/kitsu-mark-styled.svg">` instead. If the SVG is updated, refresh all five occurrences.

## What is NOT in scope

- Mobile / responsive (booth screen is 1920x1080+ landscape only)
- Localization (English only)
- Analytics, tracking, anything network beyond Google Fonts
- Build tooling
