# Icons: one style, always matched

**This rule is strict.** Icons come in one of three styles, and icons that appear together always share the same style. Mixed icon styles are one of the fastest giveaways of AI-built UI.

## The three styles
| Style | What it is | Use when |
|---|---|---|
| **Line** (outline) | Strokes only, no fills, one consistent stroke width | Most product UI. It reads light and fits dense layouts |
| **Solid** (filled) | Filled shapes, counters cut out | Bold, compact UI, small sizes, high-contrast surfaces |
| **Duotone** | A primary layer plus a secondary layer at reduced opacity (typically 30–40%) in the same hue | Illustrative or marketing-leaning UI, empty states, feature lists |

## Never mix
- **Every icon in a group shares one style.** A group is anything the eye scans together: a menu, nav bar, tab bar, sidebar, toolbar, list, card, legend, settings section, button row. No solid house next to an outline folder, and no duotone icon in a line menu.
- **The style also holds across states.** Selected, active or hover states change colour, background or weight emphasis, never the icon style. An outline icon does not turn solid when its tab is selected. If the project's own design system does swap styles on selection, flag it in the audit as a conflict and let the user decide.
- **Prefer one style for the whole product.** At minimum, keep one style per surface (app shell, content, marketing). Switching styles between surfaces must be a deliberate decision, never an accident.
- **One icon library per product.** Don't mix Lucide with Heroicons, or Font Awesome with Material Symbols. Different libraries draw different grids, corner radii and terminals, so they don't match even when both are "line".
- **No emoji as icons**, and no custom one-off glyph drawn in a different style from the set.

## Matching details within a style
| Property | Rule |
|---|---|
| Stroke (line) | One stroke width across the set (e.g. 1.5 or 2 at 24px), scaled with size, and matched to the weight of the text beside it (design hack #5). Same line caps and joins (round or square) throughout |
| Fill (solid) | Same corner rounding and counter treatment; no outline icon with a fill added by hand |
| Duotone | The same secondary opacity and the same hue relationship on every icon in the set |
| Size | Pick from a small set (16 / 20 / 24) and use one size per group; the icon box is fixed, so glyphs align on a common baseline |
| Colour | Icons in a group share one colour (state colours aside); the icon never takes a series or brand colour that the text beside it doesn't explain |
| Alignment | Centred optically on the text's x-height or cap height. Gap between icon and label from the spacing scale (6–8px) |

## Applying it (rule zero)
1. **Use the project's icon set.** Find the installed library and which styles it ships. If it only ships one style, that is the style.
2. **When the project already mixes styles,** pick the style used by most icons on the surface (or the design system's stated style), and convert the outliers to it from the same library. When the library has no matching glyph in that style, use the closest glyph that does exist in that style. Never pull a single icon from another library.
3. **Fix the source, not the screen.** If the project wraps icons in a component (`<Icon>`, a nav-item config), set the style there, so every use matches.
4. **Icon-only buttons** get an `aria-label` and a tooltip, plus the 44×44 touch target (principle #14).

## Audit checks
- [ ] One style per group (menu, nav, tab bar, toolbar, list, card)
- [ ] Style unchanged between rest, hover, selected and disabled states
- [ ] One icon library across the product
- [ ] One stroke width (line) / one secondary opacity (duotone) across the set
- [ ] One size per group, optically aligned with the label
- [ ] No emoji or one-off custom glyphs among library icons
