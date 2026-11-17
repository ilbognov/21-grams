# 10 niche design hacks

Adapted from the short video "10 Niche Design Hacks" (credited in the README).
These are small CSS-level techniques. Each entry has the rule, the before/after from the video, the code, and what to flag in an audit.

---

### 1. Concentric radius
**Rule:** A rounded element inside a rounded container must not use the same radius. Inner radius = outer radius − padding.
**Demo:** A photo card with a 48px outer radius and 18px padding. Before: the inner image also uses 48px, so the gap around the corner is thicker (25px) than along the edge (18px). After: `calc(48px - 18px)` = 30px, and the gap is an even 18px all the way round.
**Code:**
```css
.card  { --r: 48px; --pad: 18px; border-radius: var(--r); padding: var(--pad); }
.inner { border-radius: max(0px, calc(var(--r) - var(--pad))); }
```
**Flag:** The same radius on a container and its inset child. Inner radius larger than outer.

### 2. Alpha borders
**Rule:** Use translucent borders, not solid hex greys, so they work on any surface.
**Demo:** Profile cards on white, beige, blue and an orange gradient. Before: `border-color: #e4e4e7` looks pasted on top of the colour on dark and coloured cards. After: `rgb(0 0 0 / 0.12)` blends into every surface.
**Code:**
```css
--border: rgb(0 0 0 / 0.12);          /* light surfaces */
--border-on-dark: rgb(255 255 255 / 0.12);
.card { border: 1px solid var(--border); }
```
**Flag:** Hard-coded grey hex borders (`#e4e4e7`, `#e5e7eb`, `border-gray-200`) on components that sit on varied backgrounds.

### 3. OKLCH palettes
**Rule:** Build palettes in OKLCH so every hue has the same perceived lightness.
**Demo:** Six swatches, red to violet. Before: `hsl(var(--h) 90% 50%)`. They're all "50%" in HSL, but yellow and green look far brighter than blue and violet. After: `oklch(76% var(--c) var(--h))`, and all six sit at the same lightness.
**Code:**
```css
.swatch { background: oklch(76% var(--c, 0.15) var(--h)); }
/* scale: keep L fixed per step, vary h; tune c per hue to stay in gamut */
```
**Flag:** Category, tag or chart colour sets generated in HSL with one fixed lightness. Status colours that look unequally loud.

### 4. OKLCH gradients
**Rule:** Interpolate gradients in OKLCH so the middle doesn't go grey.
**Demo:** A "Golden hour" playlist card, blue `#2563eb` to orange `#f59e0b`. Before: the default sRGB blend has a muddy midpoint `#8d807b` ("goes grey in the middle"). After: `in oklch` gives a vivid pink midpoint `#df57a9` ("stays vivid the whole way").
**Code:**
```css
background: linear-gradient(90deg in oklch, #2563eb, #f59e0b);
```
**Flag:** Gradients between complementary or distant hues without an interpolation space. (Note the gram rules on gradients: use them only where the design calls for one, never as default decoration.)

### 5. Matched icon weight
**Rule:** The icon's stroke should match the weight of the text beside it.
**Demo:** A sidebar (Home, Inbox, Calendar, Team, Settings). Before: `stroke-width: 1` gives a 1.5px icon stroke next to a 3.9px text stem, which is too thin. After: `stroke-width: 2.6`, both at 3.9px, matched.
**Code:**
```css
/* scale stroke with the icon size and the text weight; Lucide-style 24px icons */
.nav svg { stroke-width: 2; }        /* 400–500 text at 14–16px */
.nav .active svg { stroke-width: 2.4; } /* 600 text */
```
Compare at 4× zoom: an icon stem should be about as thick as a letter stem in the same row.
**Flag:** Hairline icons beside medium or semibold labels. Mixed stroke widths across one icon set.

### 6. Masked edges
**Rule:** Fade the edges of horizontal scrollers instead of slicing content.
**Demo:** A "New releases" album row. Before: `mask: none`, so cards are cut off hard at the container edge. After: a gradient mask, so they fade into any background.
**Code:**
```css
.scroller {
  mask: linear-gradient(90deg, #0000, #000 15% 85%, #0000);
  -webkit-mask: linear-gradient(90deg, #0000, #000 15% 85%, #0000);
}
```
Use a smaller fade (24–48px) on dense UI. Drop the mask on the side that is at the scroll start or end.
**Flag:** Overflowing carousels and chip rows that clip mid-item with no affordance.

### 7. Blurred icon swaps
**Rule:** When one icon replaces another, blur the crossfade so it reads as one shape morphing.
**Demo:** A "Copy" button becomes "✓ Copied". Before, slowed 4×: `.out { opacity: 0 }`, so both icons are visible at once mid-swap. After: `.out { opacity: 0; filter: blur(4px) }`, which reads as one shape.
**Code:**
```css
.icon { transition: opacity 150ms ease, filter 150ms ease, transform 150ms ease; }
.icon.out { opacity: 0; filter: blur(4px); transform: scale(.8); }
.icon.in  { opacity: 1; filter: blur(0);  transform: scale(1); }
```
**Flag:** Icon state swaps (copy → check, play → pause, menu → close) done as a plain crossfade or hard cut.

### 8. Dark mode depth
**Rule:** In dark mode, higher layers are lighter. Elevation comes from lightness, not shadow.
**Demo:** A projects card with a context menu. Before: the page, card and menu all sit at `#141417` (L 19%), "all the same", so the menu disappears. After: page L 15%, card L 22%, menu `#2d2d33` at L 30%: higher = lighter.
**Code:**
```css
:root[data-theme="dark"] {
  --surface-0: oklch(15% 0.005 270);  /* page */
  --surface-1: oklch(22% 0.005 270);  /* card */
  --surface-2: oklch(30% 0.006 270);  /* menu, popover, modal */
}
```
**Flag:** Dark themes where card, menu and page share one background. Shadows used as the only elevation cue in dark mode.

### 9. Dynamic viewport
**Rule:** Use `dvh`, not `vh`, for full-height mobile layouts.
**Demo:** A phone hero, "Dinner, sorted." Before: `.hero { height: 100vh }` sizes to the viewport with the toolbar hidden, so the "Book a table" button is hidden under the browser toolbar. After: `100dvh` fits what you see.
**Code:**
```css
.hero { min-height: 100svh; min-height: 100dvh; }  /* svh fallback, dvh where supported */
```
Use `svh` for things that must never move, `dvh` for things that should track the toolbar, and `lvh` rarely.
**Flag:** `100vh` / `h-screen` on mobile full-height screens, sheets or sticky bottom CTAs.

### 10. Multiply blending
**Rule:** Product shots on white backgrounds: use `mix-blend-mode: multiply` so the white disappears into a tinted surface.
**Demo:** Product cards (Clay vase, Amber candle, Glass bottle) on a beige panel. Before: `normal`, with a white box around each photo. After: `multiply`, and the white just disappears.
**Code:**
```css
.product img { mix-blend-mode: multiply; }
/* dark surfaces: use screen on dark-background shots, or a transparent PNG/WebP */
```
**Flag:** White-background product or logo images sitting in visible white boxes on non-white cards.

---

## Quick audit checklist

| # | Check | Pass when |
|---|---|---|
| 1 | Nested radius | inner = outer − padding |
| 2 | Borders | alpha colour, not solid grey hex |
| 3 | Palettes | OKLCH, equal lightness per step |
| 4 | Gradients | `in oklch`, no grey midpoint |
| 5 | Icons | stroke matches adjacent text weight |
| 6 | Scrollers | edge mask fade, no hard slice |
| 7 | Icon swaps | blur + opacity crossfade |
| 8 | Dark mode | higher layer = lighter surface |
| 9 | Mobile height | `dvh`/`svh`, never bare `vh` |
| 10 | Product images | multiply on tinted surfaces |
