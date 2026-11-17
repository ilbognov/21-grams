# Toggles: switches and segmented controls

Use the project's existing switch and segmented control when it has them, and apply these specs through their styles or props. Build new ones only when they don't exist.

## Switch (on/off)
| Part | Spec |
|---|---|
| Track | 44 × 26, fully round. On = accent. **Off = a grey with at least 3:1 against the surface** (e.g. `#838ea4` on white: 3.3:1, meets the non-text contrast rule) |
| Knob | 20px white, `0 1px 2px rgb(7 29 73 / .3)` shadow, 3px inset |
| Travel | 18px via `translate`, **200ms `cubic-bezier(.4,0,.2,1)`** |
| Stretch | while moving, `scale: 1.12 .89` at the midpoint (area kept, craft #5). While pressed, it holds the stretched shape so the tap registers |
| Track colour | 120ms ease-out |
| Row | the whole row is the target (a `<label>`), at least 64px tall: title 16/500 and description 14 muted. Hover is a soft wash. Rows are split by inset hairlines, with no box around the list |
| Semantics | native `<input type="checkbox" role="switch">` and a visible focus ring |

Use the CSS `translate` and `scale` properties rather than one `transform`, so the travel transition and the stretch animation don't fight.

## Segmented control (2–4 options)
Depth, not outlines, shows what's selected: the track sits low, the selected option sits high.

| Part | Spec |
|---|---|
| Track | **no border.** Filled with the regular border colour (about 9% ink, e.g. `rgb(21 32 51 / .09)`), radius 8, 2px padding. Keep it soft: the strong border colour (16%+) reads as a dark block |
| Indicator | the page or card colour (white in light), radius 6 (outer 8 − padding 2), a small shadow (`0 1px 2px rgb(0 0 0 / .1)`) so it reads as raised. **Slides 200ms ease-in-out** to the chosen option |
| Unselected | flat on the track, no fill or border. Labels 14/500 in a secondary ink that **still passes 4.5:1 on the track** (measure it: the track is darker than the page) |
| Selected label | 600, ink, drawn by a **mask layer that travels with the indicator** (craft #17). Hide the base label under the selected option to avoid a doubled glyph |
| Dark mode | the track **sinks** (slightly darker than its surroundings, e.g. ~18% black) and the indicator **rises** (one step lighter). Never the reverse, or the selection looks pressed in |
| Disabled | faint text, `not-allowed`, and a `title` giving the reason ("Not available yet") |
| Semantics | `role="radiogroup"` with `role="radio"` + `aria-checked` buttons |

Pairs of buttons that behave as a toggle (Bars / Trend lines) use this same style.

Use a segmented control for view switches (Chart / Table, date range). Use a switch only for settings that take effect immediately.
