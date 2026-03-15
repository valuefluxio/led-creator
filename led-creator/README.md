# LED Screen Content Creator

A single-file browser tool for creating, previewing, and exporting animated content for LED screens.

**Live:** https://led-creator.vercel.app

---

## Overview

LED screens have a pixel pitch (e.g. P4 = 4mm between pixels) and a physical size (e.g. 4m × 2m), which together determine the exact screen resolution (4000mm ÷ 4mm = 1000px wide). This tool renders a canvas at that exact resolution so you can preview and export content with pixel-perfect accuracy.

---

## Setup

1. Open the app — a setup modal appears
2. Enter **Screen Width** and **Screen Height** in meters
3. Select **LED Pixel Pitch** from the dropdown (P1.5 → P20), or choose **Custom…** to enter any value in mm
4. The live preview shows the calculated resolution and total pixel count
5. Click **Create Content →**

The ✎ Edit button in the top bar reopens the modal at any time.

---

## Animation Modes

| Mode               | Description                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **Color Test**     | Standard broadcast test pattern — 7 color bars, grayscale ramp, black/red/white strip, crosshair, corner markers |
| **Scroll Text**    | Text scrolls horizontally across the screen. Configure text, color, background, and font size                    |
| **Color Sequence** | Define a list of colors with per-step durations and optional fade transitions                                    |
| **Patterns**       | Animated geometric patterns: Pulse, Wave, Sweep, Checkerboard, Sparkle                                           |
| **Images**         | Upload one or more images and set a display duration per frame                                                   |

### Color Test extras

- **Breathing** — subtle ±5% brightness pulse on color bars
- **Cycle** — press `Space` or click the Cycle button to toggle a full-screen R → G → B → White → Black cycle (useful for LED calibration)

---

## Export Video

1. Click **⬇ Export** in the toolbar
2. Set **Loop Duration** (2s / 5s / 10s / 20s) — defines the full length of one animation cycle
3. Drag the **in** and **out** handles on the timeline to select the exact range to export
4. Click **⏺ Record** — the animation seeks to the in-point and records at 30fps
5. The file downloads automatically when done

**Format:** MP4 where supported by the browser, WebM otherwise. WebM can be converted to MP4 with [HandBrake](https://handbrake.fr) or any video converter.

### Info overlay

The exported video has a burned-in info panel (bottom-right corner) showing:

- LED Pitch
- Screen Size
- Resolution
- FPS
- Bitrate

---

## Using on an Actual LED Screen

**Option A — Direct connection (no export needed)**
Connect the LED screen as a second monitor, open the app in a browser, click ⛶ Full to go fullscreen, then drag the window to the LED display. The canvas renders at exact pixel resolution.

**Option B — Video file**
Export a video and load it into the screen's media player software (NovaStudio, Verypixel, etc.).

---

## Resolution Formula

```
pixelsWide = round((widthMeters × 1000) / pitchMm)
pixelsTall  = round((heightMeters × 1000) / pitchMm)
```

**Example:** 4m × 2m screen at P4 → 1000 × 500 px

---

## Project

```
led-creator/
└── index.html    # entire app — no dependencies, no build step
```

**Deploy:**

```bash
vercel --prod
```
