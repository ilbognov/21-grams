# 6g · Colour: one accent

House default: one accent, and **button text must pass WCAG AA contrast** in every theme. The accent is always the project's brand colour.

## Where colour goes
- **Accent** (the brand colour) appears only on: the accent primary action (if used), focus rings, selection and active states, links in running text. One accented thing per region.
- **Status colours** (green ok, amber warning, red error, blue info) are separate from the accent and are never used for decoration. A positive delta is green, not brand.
- **Neutrals** carry everything else: page, surfaces, text, borders.
- Build palettes and gradients in OKLCH (hacks #3 and #4). Borders are alpha (hack #2).

## Contrast (non-negotiable)
| Pair | Minimum |
|---|---|
| Button and badge text on its fill | 4.5:1 (AA), in **both themes** |
| Body text on surface | 4.5:1 |
| Large text (≥ 18px, or ≥ 14px/600) | 3:1 |
| Focus ring and UI boundaries against neighbours | 3:1 |

**Check it, don't eyeball it.** A typical failure: a dark-mode accent lightened for legibility (e.g. `#7FA4FF`) with white text gives **2.43:1 (fail)**. The same fill with near-black text (`#0B1220`) gives **7.72:1**. So:
- Define `--on-accent` per theme. It is white on a dark accent and near-black on a light accent.
- Light theme `#2457D6` + white = 6.16:1 ✓
- If a brand colour can't reach 4.5:1 with either text colour, darken or lighten the fill. Don't shrink the text.

```css
:root { --accent: #2457D6; --on-accent: #FFFFFF; }
:root[data-theme="dark"] { --accent: #7FA4FF; --on-accent: #0B1220; }
```

## Never
Purple/indigo-to-violet gradients by default, gradient text, brand-tinted whole surfaces, the brand colour on the badge, number and button in one card, `gray-500` for secondary text, status shown in brand colour.
