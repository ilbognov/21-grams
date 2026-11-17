# 10 typography hacks

Adapted from the short video "10 Niche Typography Hacks" (credited in the README).
Small, CSS-level typography details. Each entry has the rule, the before/after from the video, the code, and what to flag in an audit. They sit on top of `rules/type.md` (scale, weights, tracking).

---

### 1. Reserved bold width
**Rule:** Text that turns bold on hover or selection must not change width, or the whole row shifts.
**Demo:** Tabs (Overview, Analytics, Customers, Settings). Before: hovering a tab makes it bold, it grows and the whole row jumps (moved 6px, then −4px). After: nothing moves.
**Code:** stack a hidden bold copy of the label in the same grid cell, so the box is always as wide as the bold version.
```css
.tab { display: inline-grid; }
.tab > *, .tab::after { grid-area: 1 / 1; }
.tab::after { content: attr(data-text); font-weight: 700; visibility: hidden; }
```
```html
<a class="tab" data-text="Customers"><span>Customers</span></a>
```
**Flag:** Tabs, nav items, segmented controls or filters whose weight changes on hover or select and nudge their neighbours. Alternative: change colour or background only, not weight.

### 2. Text-box trim
**Rule:** Trim the font's built-in leading so text sits optically centred in buttons, badges and pills.
**Demo:** A "BOOK A TABLE" button. Before: the line box leaves room for descenders, so caps sit too high (66px above vs 84px below). After: dead centre (75 / 75).
**Code:**
```css
.label { text-box-trim: trim-both; text-box-edge: cap alphabetic; }
```
Use it on single-line labels in boxes (buttons, badges, chips, avatars with initials). It's progressive: browsers without support keep today's rendering, so keep padding sensible.
**Flag:** All-caps or single-line labels that look high in their box. Padding hacks (`padding-top: 1px`) used to fake centring.

### 3. Underline offset
**Rule:** Push link underlines below the descenders.
**Demo:** "Typography guide" link. Before: the default underline cuts through every g and y ("chopped up"). After: `0.2em` offset, the line clears every letter.
**Code:**
```css
a { text-underline-offset: 0.2em; text-decoration-thickness: from-font; }
```
**Flag:** Links with `text-underline-offset: auto` on fonts with deep descenders; underlines faked with `border-bottom`.

### 4. Superscript spacing
**Rule:** Superscripts must not push their line apart.
**Demo:** Pricing fine print with footnote markers. Before: lines with a superscript are taller (56 / 63 / 56 / 63px, "uneven lines"). After: an even 56px rhythm.
**Code:**
```css
sup { line-height: 0; position: relative; vertical-align: baseline; top: -0.5em; }
sub { line-height: 0; position: relative; vertical-align: baseline; top: 0.25em; }
```
**Flag:** Uneven line spacing in paragraphs with footnotes, ®, ™ or exponents.

### 5. Fluid type
**Rule:** Large display headings scale smoothly with the viewport instead of snapping at breakpoints.
**Demo:** "Type that fits every screen." Before: `font-size: 40px` jumps between 68px and 40px at a breakpoint. After: `clamp()` scales smoothly (55px, 40px, 39px…).
**Code:**
```css
h1 { font-size: clamp(2rem, 1rem + 5vw, 4rem); }
```
**Scope:** only hero and display headings (roughly 28px and up). UI text, from labels and body to panel titles, stays on the fixed scale in `rules/type.md`, so components stay predictable. Always include a `rem` term so zoom still works.
**Flag:** Display headings that jump sizes at breakpoints; `vw`-only font sizes (break zoom).

### 6. Small-caps acronyms
**Rule:** Set runs of capitals (acronyms, file types) in small caps so they don't shout inside a sentence.
**Demo:** "Connect your CRM over our REST API, then export every report as CSV or PDF." Before: full caps look like shouting. After: `all-small-caps` blends into the sentence at x-height.
**Code:**
```css
abbr, .acronym { font-variant-caps: all-small-caps; letter-spacing: 0.02em; }
```
```html
<abbr title="Customer relationship management">CRM</abbr>
```
Use only when the font has real small caps (most good text faces do); otherwise leave caps as they are. Not for UI labels, codes or IDs users must type.
**Flag:** Paragraphs dense with full-caps acronyms.

### 7. Curly quotes
**Rule:** Use real punctuation: curly quotes and apostrophes, not typewriter marks.
**Demo:** A testimonial. Before: `"It's the only app I've kept…"` with straight marks. After: `“It’s the only app I’ve kept…”`.
**Code:** a text change, not a CSS property. Use `“ ” ‘ ’` in copy and `’` for apostrophes; `–` for ranges, `—` sparingly, `…` for ellipses, `×` for dimensions. In JSX, write the characters directly (or `&rsquo;`), and keep straight quotes only inside code.
**Flag:** `"` and `'` in UI copy, testimonials, headings; `...` instead of `…`; hyphens in numeric ranges (`10-20` → `10–20`).

### 8. Middle truncation
**Rule:** When the end of a string tells items apart (file names, paths, IDs), truncate the middle, not the end.
**Demo:** An uploads list. Before: `Q4 board update final ve…` twice ("Which one?"). After: `Q4 board update fina….pdf` and `….key`, so the extension stays visible.
**Code:** split the name and keep the tail from shrinking:
```css
.file { display: flex; min-width: 0; }
.file .name { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.file .ext  { flex-shrink: 0; }
```
```html
<span class="file"><span class="name">Q4 board update final version</span><span class="ext">.pdf</span></span>
```
Put the full name in a `title` or tooltip.
**Flag:** Lists where end-truncated items look identical; file names whose extension disappears.

### 9. Auto hyphenation
**Rule:** Narrow, justified or long-word columns use the browser's hyphenation, with the page language set.
**Demo:** "Field notes" in a narrow card. Before: `hyphens: manual` leaves rivers of white (biggest gap 201–205px vs a normal 9px space). After: `lang="en"` + `hyphens: auto`, the biggest gap drops to 29–49px.
**Code:**
```html
<html lang="en">
```
```css
p { hyphens: auto; hyphenate-limit-chars: 7 3 3; }
```
Only for running text in narrow columns. Never hyphenate headings, buttons, labels, names or code. Prefer left-aligned (ragged) text over justified in product UI.
**Flag:** Missing `lang` on `<html>`; justified narrow text with large gaps.

### 10. Line-clamped titles
**Rule:** Titles in a grid of cards are clamped to a fixed number of lines so the cards line up.
**Demo:** Three article cards. Before: titles run 2–4 lines, so the meta line sits at different heights ("ragged grid"). After: every title clamped to 2 lines with an ellipsis, so the meta lines align.
**Code:**
```css
h3 { display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 2; overflow: hidden; }
/* or, where supported: */
h3 { line-clamp: 2; }
```
Give the full title in a `title` attribute or on the detail page. Clamp only where alignment matters (grids, carousels), not in reading content.
**Flag:** Card grids with ragged title heights; titles cut with a fixed `height` instead of a line clamp.

---

## Quick audit checklist

| # | Check | Pass when |
|---|---|---|
| 1 | Bold on hover/select | no layout shift (hidden bold copy reserves width) |
| 2 | Labels in boxes | optically centred (`text-box-trim`) |
| 3 | Links | underline clears descenders (`0.2em` offset) |
| 4 | Footnotes / exponents | line rhythm unchanged |
| 5 | Display headings | fluid `clamp()` with a `rem` term; UI text on the fixed scale |
| 6 | Acronyms in prose | small caps when the font has them |
| 7 | Punctuation | curly quotes, real apostrophes, en dashes, ellipsis character |
| 8 | Truncated names | middle-truncated, distinguishing tail kept |
| 9 | Narrow running text | `lang` set, `hyphens: auto`, no rivers |
| 10 | Card titles in grids | clamped to the same line count |
