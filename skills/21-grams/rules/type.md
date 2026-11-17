# 4g · Type: few sizes, tight headings

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Families
- **The project's fonts come first.** Keep its brand typefaces and apply the scale, weights and tracking below.
- Default when the project has none: **Geist** for UI (`"Geist", ui-sans-serif, system-ui, -apple-system, "Segoe UI", sans-serif`) and **Geist Mono** for numbers, IDs, timestamps and code.
- Use `tabular-nums` wherever digits line up.

## Scale (use only these)
| Token | Size / line-height | Weight | Tracking | Use |
|---|---|---|---|---|
| `--text-xs` | 12 / 16 | 400–500 | 0 | meta, captions, table headers |
| `--text-sm` | 14 / 22 (1.55) | 400 | 0 | body, controls |
| `--text-md` | 16 / 24 | 500 | −0.006em | emphasised body, section labels |
| `--text-lg` | 22 / 28 | 600 | −0.022em | panel and page titles |
| `--text-xl` | 28 / 32 | 600 | −0.025em | page hero titles (rare) |

At most **four sizes per screen**. Weights are only 400, 500 and 600.

## Mobile headings
On phone layouts (< 768px), headings go up one step so they read at arm's length:

| Heading | Desktop | Mobile |
|---|---|---|
| Section heading (e.g. "Recent activity") | 16 / 24, 600 | **18 / 24, 600**, −0.015em |
| Card heading (e.g. "Top issues", "Team members") | 14 / 20, 600 | **16 / 22, 600** |
| Page title | 28 / 32 | 22 / 28 (when shown in the body; a header title stays 16) |

Body and meta sizes do not change. A mobile screen then uses 18 / 16 / 14 / 12, which is still four sizes.

## Secondary text
- Secondary: ink at about 70% (`--ink-2`). Tertiary and meta: about 50% (`--ink-3`). Both are mixed from the ink colour, never Tailwind `gray-500`.
- Must still pass 4.5:1 for body sizes (3:1 for 18px+ or 14px/600+).

## Rules
- Headings get `text-wrap: balance`. Body is at most about 65ch wide.
- Sentence case everywhere. Uppercase is only for tiny mono labels (+0.06em), if at all.
- Long numbers are chunked (principle #16): `4532 0151 1283 0366`.

## Never
Gradient text, a 30px+ bold headline in product UI, wide-tracked bold coloured eyebrows, Inter at default tracking as an unconsidered default, more than one display face.
