# LED Screen Content Creator — Dev Log

**Built by ValueFlux**

---

## Links

|                  | URL                                                                  |
| ---------------- | -------------------------------------------------------------------- |
| **App**          | https://led-creator.vercel.app                                       |
| **Presentation** | https://presentations-delta-seven.vercel.app/led-creator-slides.html |
| **GitHub**       | https://github.com/valuefluxio/led-creator                           |

---

## Development History

### 2026-03-15 — Initial Build

Built the entire app as a single HTML file with no dependencies or build step.

**Core features shipped:**

- Setup modal — screen width/height (meters) + LED pitch dropdown (P1.5 → P20)
- Live resolution preview in modal: `pixelsWide = round((widthM × 1000) / pitchMm)`
- Canvas rendered at exact pixel resolution, CSS-scaled to fit browser window
- Color Test pattern — 7 color bars, grayscale ramp, black/red/white strip, crosshair, corner markers
- Breathing animation on color bars (±5% brightness, 2s cycle)
- Color Cycle mode (R → G → B → White → Black) toggled via Space key or button
- Scroll Text mode — configurable text, color, background, font size
- Color Sequence mode — list of colors with per-step durations and optional fade
- Moving Patterns mode — Pulse, Wave, Sweep, Checkerboard, Sparkle
- Image Sequence mode — upload images, set display duration per frame
- Play/Pause control
- Fullscreen button

---

### 2026-03-15 — Bug Fix: Space Key Toggle

**Problem:** Pressing Space to toggle Color Cycle mode didn't work.

**Root cause:** Browser fires a `click` event on `keyup` for any focused `<button>`. The `keydown` handler toggled the mode, but the browser-generated click immediately toggled it back.

**Fix:** Added a `keyup` listener that calls `preventDefault()` when Space is pressed on a button, blocking the deferred click.

---

### 2026-03-15 — Feature: Video Export

Added MP4/WebM export via `MediaRecorder` API with `canvas.captureStream(30)`.

- Loop Duration picker (2s / 5s / 10s / 20s)
- In/out point timeline with draggable handles
- Animation seeks to in-point before recording starts
- File downloads automatically on completion
- MP4 where browser supports it, WebM fallback

---

### 2026-03-15 — Bug Fix: Play Button State

**Problem:** Play button showed `▶` on load, implying content wasn't playing — users clicked it immediately and stopped the animation.

**Fix:** Changed initial HTML to `⏸` and corrected the textContent toggle logic.

---

### 2026-03-15 — Feature: Info Overlay on Exported Video

Burned-in info panel (bottom-right) appears on every exported video showing:

- LED Pitch
- Screen Size
- Resolution
- FPS (measured via rolling 1s counter using `performance.now()`)
- Bitrate

---

### 2026-03-15 — Feature: Custom LED Pitch

Added `Custom…` option to the pitch dropdown that reveals a number input for any mm value beyond the preset list (P1.5 → P20).

---

### 2026-03-15 — Deploy & Docs

- Initialized git repo at `~/yeonFlux/yeonCode/`
- Deployed app to Vercel: **https://led-creator.vercel.app**
- Created `README.md` documenting setup, animation modes, export workflow, and resolution formula

---

### 2026-03-15 — Presentation

Created a 9-slide trilingual presentation (EN / KO / JA) at `presentations/led-creator-slides.html`.

- Dark theme matching the app (`#0a0a0a` bg, `#00d4ff` cyan, `#ff6b35` orange)
- Fonts: Space Grotesk + Space Mono
- Language switcher (top-right buttons), preference saved to `localStorage`
- Floating LED pixel canvas background animation
- Slides: Title, Overview, Resolution Formula, Setup, Animation Modes, Export Video, Info Overlay, Real Screen Usage, Tech & CTA
- Deployed to: **https://presentations-delta-seven.vercel.app/led-creator-slides.html**

---

### 2026-03-15 — Polish

- CTA "Open in browser →" button on final slide redesigned as a solid orange gradient button with glow and hover animation
- Copyright notice added to both app (toolbar) and presentation (fixed footer): `© 2026 ValueFlux · All Rights Reserved`
- Presentation title slide updated to: **ValueFlux Presents / LED Screen Content Creator**

---

### 2026-03-15 — GitHub

- Created public repo: **https://github.com/valuefluxio/led-creator**
- Pushed full commit history

---

### 2026-03-15 — Presentation Polish

- Language toggle buttons (EN / KO / JA) resized — font `0.68rem → 0.85rem`, padding increased for easier tapping
- Presentation title updated to match app: **LED Screen Content Creator**
- Eyebrow text on title slide set to **ValueFlux Presents**
- Copyright text color made visible across both app and presentation

---

### 2026-03-15 — Mobile Browser Notice

Added a full-screen overlay shown on screens under 768px wide:

- Informs mobile users the tool is designed for desktop
- Shows the live URL for easy copy on desktop
- **"Proceed on mobile browser"** button dismisses the notice and allows full access anyway

---

## Tech Stack

| Concern   | Approach                                     |
| --------- | -------------------------------------------- |
| Runtime   | Single HTML file, zero dependencies          |
| Rendering | Canvas 2D API                                |
| Animation | `requestAnimationFrame` loop                 |
| Export    | `MediaRecorder` + `canvas.captureStream(30)` |
| Scaling   | CSS `transform: scale()` via `ScaleManager`  |
| Deploy    | Vercel CLI (`vercel --prod`)                 |
