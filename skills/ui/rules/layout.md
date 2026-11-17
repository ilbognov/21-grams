# Layout: lists, screen actions and the logo

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Row lists are one table (strict)
When a screen shows a table-like list (many rows, each drawn as its own bordered or shadowed card with a small gap between them), merge the rows into **one container**.

| Part | Spec |
|---|---|
| Container | one surface, radius 12, `overflow: hidden` (keep `overflow: auto` on lists that scroll) |
| Rows | no gap, no radius of their own, no border or shadow. The first row carries the top corners and the last row the bottom ones |
| Dividers | a 1px horizontal hairline between rows in the alpha border colour, none after the last row |
| Hover | a fill step on the row, never a border, shadow or lift |
| Selected / expanded | a tinted fill shared by the row and its expanded detail, so they read as one unit. No coloured outline |
| Focus | ring inside the row (`outline-offset: -2px`) so the container doesn't clip it |

Applies to patient, order and user lists, file lists, and pickers in dialogs. **Multi-column card grids stay separate cards.**

```css
.list { border-radius: 12px; overflow: hidden; background: var(--surface); }
.list > .row { border-radius: 0; margin: 0; box-shadow: none; border: 0; }
.list > .row + .row { border-top: 1px solid var(--border); }
.list > .row:hover { background: var(--surface-hover); }
```

## Screen actions sit top right (strict)
Actions that act on the whole screen or window (Copy, Export, Share, Open PDF, New…) are **one group at the right edge of that screen's header**.

- Order: secondary actions first, the **one solid primary last, in the corner**.
- Icon + verb-object label ("Copy values", "Open PDF"). Wrap the group in a labelled container (`role="group"` with an `aria-label` naming the screen) so it's announced as this screen's actions.
- **Never mix actions into selectors.** Date pickers, report pickers, filters and pagination stay in their own bar; actions don't sit between them.
- **Remove duplicates** further down the screen (a card's own "Copy" that does the same as the header's).
- Actions that belong to one card (a chart's view toggle, a row's menu) stay in that card.
- Mobile: the group wraps to a full-width row under the title, buttons 40px tall, primary on the right.

## The logo
- **If the product has no real logo** (an initials tile, a letter in a gradient square, a generic icon standing in for the brand), **ask the user for theirs during the audit** (SVG preferred) instead of polishing the placeholder. Initials in a user's avatar aren't a logo; leave those alone.
- Use the logo exactly as supplied: keep the proportions between the mark and the wordmark and their gap, and centre them on each other. No tile, gradient, glow or shadow behind it.
- The wordmark follows the theme's ink colour (dark in light mode, light in dark mode) when it's a single-colour wordmark. A coloured mark stays as is if it holds 3:1 on both backgrounds.
- A collapsed sidebar shows the mark only. The mark can double as the favicon.
