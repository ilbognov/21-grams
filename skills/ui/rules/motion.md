# 3g · Motion: smooth, from the trigger, no bounce

Everyday UI enters from its trigger with a slight scale and a soft landing, leaves faster than it came, and never bounces. Full detail for each technique is in `references/animation-craft.md`. Use the project's animation library if it has one; otherwise CSS transitions.

## Tokens
| Token | Value | Use |
|---|---|---|
| `--ease-out` | `cubic-bezier(.2, 0, 0, 1)` | all entrances |
| `--ease-in` | `cubic-bezier(.4, 0, 1, 1)` | all exits |
| `--ease-move` | `cubic-bezier(.4, 0, .2, 1)` | moving from A to B on screen |
| `--dur-press` | 150ms | press scale |
| `--dur-fast` | 120ms | hover colour, icon swaps |
| `--dur-menu` | 220ms | menus, dropdowns, popovers, tooltips (150–250 range) |
| `--dur-menu-exit` | 175ms | ≈ 80% of `--dur-menu` |
| `--dur-panel` | 240ms | drawers, sheets, dialogs, accordions |
| `--dur-panel-exit` | 190ms | ≈ 80% of `--dur-panel` |
| `--stagger` | 30ms | list rows on open, capped at ~6 rows |
| `--trail` | 50ms | secondary details settling after the body |

## Recipes
- **Menu / popover / dropdown:** `transform-origin` at the trigger. Enter from `opacity 0; scale(.95)` over `--dur-menu --ease-out`, with rows staggered 30ms. Exit back toward the trigger: `scale(.95)` + opacity over `--dur-menu-exit --ease-in`. **No overshoot.**
- **Dialog:** scrim fades over `--dur-panel`. Dialog enters from `scale(.96)` + opacity with `--ease-out`, no overshoot. Exit over `--dur-panel-exit`.
- **Toast:** enters 8px from its edge with `--ease-out`. Contents trail by 50ms.
- **Button press:** `scale(.97)` over `--dur-press` plus the colour step (see buttons.md). Hover: colour only.
- **Toggle and slider knob:** ~12% area-preserving stretch while travelling (`scaleX 1.12 / scaleY .89`).
- **State swaps (Save → Saved, tabs):** old and new overlap, with no blank frame between them. Icons: scale + opacity + `blur(4px)`.
- **Segmented controls and tabs:** the indicator moves with `--ease-move`. The active label colour is revealed by a clip or mask that travels with it.
- **Success:** one pulse (ring 0 → 8px fading out, 400ms). Never loop.
- **Error:** shake ±6px, 3 cycles, about 300ms, plus text.
- **Travel (add to cart, move file):** an arc (~32px lift), `--ease-move`.
- **Card → detail:** the same element expands (shared `layoutId` / view transition). Never a disconnected replacement.
- **Drag:** 1:1 with the pointer, no transition while held. Rubber band past bounds, then settle with `--ease-out` on release.

## Limits
- **No spring overshoot or wobble on everyday UI** (menus, popovers, dialogs, panels, tabs, toasts). Bounce is allowed only for rare, playful moments the user asks for.
- No motion on high-frequency interactions (keyboard navigation, list and palette highlight, tabs in tools): instant, or 60ms opacity at most (principle #20).
- No fade-up-on-scroll and no page-load stagger for content. The 30ms stagger is only for lists inside a surface that just opened.
- No hover scale on cards or buttons.
- Never `scale(0)` entrances. Never centre-origin popovers.
- Animate only `transform`, `opacity`, `filter` and `clip-path`.
- Nothing user-triggered takes longer than 300ms to settle.
- `prefers-reduced-motion: reduce`: remove translate, scale, stretch and stagger. Keep opacity at `--dur-fast`.

```css
@media (prefers-reduced-motion: reduce) {
  :root { --dur-menu: 120ms; --dur-menu-exit: 100ms; --dur-panel: 120ms; --dur-panel-exit: 100ms; --stagger: 0ms; --trail: 0ms; }
  * { --motion-scale: 1; --motion-distance: 0px; }
}
```
