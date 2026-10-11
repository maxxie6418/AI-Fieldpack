# Rendering the canvas

> **Added by AI Fieldpack.** This file is not part of the upstream `canvas-design` package.

`SKILL.md` defines *what* to make — a design philosophy (`.md`) and a piece of artwork (`.pdf` or `.png`). It never says how to turn a design into a file. This reference fills that gap: fonts, three interchangeable output routes, and the checks to run before calling the work finished.

## 1. Fonts

Use the fonts bundled in `../canvas-fonts` first — 54 static weights across 27 families, each family shipping its own `*-OFL.txt` under the SIL Open Font License 1.1.

- Some of those licences carry a **Reserved Font Name** clause: keep the font files under their original names, and keep each `*-OFL.txt` next to the font it covers. Do not rename or re-subset a font under a different name.
- Only fetch an additional font when the piece genuinely needs one that is not bundled, and only when its licence is clear. `SKILL.md`'s "download whatever fonts are needed" is the fallback, not the first move.
- **Never let the renderer fall back to a system font silently.** A poster that quietly typesets itself in Arial is the most common way this skill fails. If a requested family cannot be resolved, stop and say so.

## 2. Pick an output route

Choose the first route the environment actually supports. All three produce the same deliverable; none is preferred for aesthetic reasons.

### Route A — HTML or SVG, rasterized by a headless browser

Write one self-contained `.html` (or `.svg`) file, then render it. Text stays real text, and bundled fonts load from `../canvas-fonts` via `@font-face`.

```bash
# PNG at an exact canvas size
chrome --headless --disable-gpu --hide-scrollbars \
  --screenshot=poster.png --window-size=1200,1600 poster.html

# PDF, keeping vector quality; --no-pdf-header-footer drops the URL and date
chrome --headless --disable-gpu --no-pdf-header-footer \
  --print-to-pdf=poster.pdf poster.html
```

- Microsoft Edge (`msedge`) accepts the same flags. Typical Windows locations:
  - `C:\Program Files\Google\Chrome\Application\chrome.exe`
  - `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe`
- Newer builds also accept `--headless=new`; plain `--headless` remains a valid alias.
- The screenshot is taken at the viewport, not the document: set `--window-size` to the canvas size and let the page fill it exactly.
- For PDF, control the page box with print CSS — `@page { size: 1200px 1600px; margin: 0; }` — otherwise the browser applies A4 and rescales the composition.
- Multi-page: either print one tall page and let the PDF paginate, or render one PNG per page and keep the set together.

### Route B — Draw directly with Pillow (no browser required)

When no headless browser is available, compose the piece in Python. Pillow writes PNG directly and a single-page PDF on its own.

```python
from PIL import Image, ImageDraw, ImageFont

W, H = 1200, 1600
img = Image.new("RGB", (W, H), "#f4f1ea")
d = ImageDraw.Draw(img)
font = ImageFont.truetype("../canvas-fonts/BigShoulders-Regular.ttf", 180)
d.text((96, 120), "CHROMATIC SILENCE", font=font, fill="#111111")
img.save("poster.png")
img.save("poster.pdf", "PDF", resolution=300)
```

Pillow's PDF output is a raster page, not vector — for type-led work that must stay crisp at any size, prefer Route A.

### Route C — No renderer at all

Deliver the `.html` / `.svg` source, plus one line naming what to open it with. State plainly that no `.png` or `.pdf` was produced. **Never claim an image file exists when it does not** — a wrong deliverable costs far more than an honest one.

## 3. Before calling it finished

- Canvas size is fixed in the source, and every element sits inside the margins: nothing clipped, nothing overlapping.
- Fonts resolve from `../canvas-fonts` or from an explicitly fetched file — never a silent fallback.
- The `.md` philosophy and the artwork ship together.
- The rendered file opens and looks the way the source says it should. Open it before delivering it.
