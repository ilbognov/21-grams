# Charts: line, column, horizontal bar

Use the project's chart library and its configuration (Recharts, visx, Chart.js, ECharts, hand-rolled SVG…); never add a new one. If a data-visualisation skill is installed, load it too.

## Colour
- **Series colours never borrow the status colours.** Green, amber and red mean healthy, watch and at risk. A series coloured green reads as "good". Use a categorical palette that starts from the brand colour, for example `#0066f5 · #eb6834 · #1baf7a` on white.
- **One measure, one hue.** A ranked bar chart uses the brand colour for the bar the story is about and a lighter step (`#86b6ef`) for the rest. Never give each bar its own colour.
- **Check every categorical palette** for colour-blind separation and contrast against the surface (a palette validator or a CVD simulator). A colour under 3:1 against the surface needs direct labels or a table view.
- Text never wears the series colour. Values and labels use the ink colours, and identity comes from a line key or dot beside the text.

## Marks
| Mark | Spec |
|---|---|
| Line | 2px, round join. End dot r 4 with a 2px white ring |
| Column / bar | ≤ 24px thick, 4px rounded data end, square at the baseline |
| Area | series hue at 10% |
| Grid | 1px solid hairline `rgb(7 29 73 / .08)`; baseline `/ .22` |
| Ticks | 3–5 clean values (`0%, 0.2%, 0.4%…`, `0, 1,000, 2,000`), 12px muted, tabular figures |

## Labels
- Label line ends directly with the latest value and the series name. With ≤ 4 series, keep a small line-key legend too.
- Columns: label only the peak and the latest value. Horizontal bars: value at every tip.
- Month axis: every 2nd month (3rd on phones) plus the latest. Drop a regular label that would crowd the latest.
- No rotated axis titles. The card title names the measure, and a one-line subtitle states the takeaway ("Error rate fell from 0.8% to 0.4% this year.").
- Convert awkward units into readable ones: 0.00459% per order becomes **4.59 per 100,000 orders**. Keep the exact value in the tooltip.

## One scale per chart
- **Never plot two measures on one axis or on a hidden second axis.** Orders and revenue become **two charts that share the x-axis** (small multiples), each with its own scale, aligned so the months line up.

## Interaction
- Line charts: a crosshair snaps to the nearest month, and one tooltip lists every series (values lead, names follow, line keys).
- Columns and bars: the mark is the target, lifting slightly on hover. Rows in a horizontal bar chart get a soft hover wash.
- **Segmented marks get a breakdown panel, not a native tooltip.** A stacked or segmented bar (ranges, zones, a budget split) opens a small floating panel on hover instead of the browser's `title` text:
  - header: what the bar is (the entity's name) with its context underneath (date range, count of segments);
  - one row per segment **in the same order the product uses elsewhere**, each with a colour key, name, range or definition, a small proportional bar and the value (tabular figures);
  - the row under the pointer is highlighted as the pointer moves along the bar;
  - totals only when they add information; no verdicts or targets the product doesn't make;
  - it opens below the mark and flips above near the bottom of the viewport, never runs off an edge, grows from the mark (220ms in / 175ms out, opacity only with reduced motion) and closes on leave, scroll or click;
  - touch screens skip the panel; tapping does what clicking did.
- Linked charts share hover: hovering a month in one highlights it in the other, with a single tooltip.
- Charts are focusable. Arrow keys move the crosshair and Esc clears it.
- Every chart offers a **Chart / Table** toggle (segmented control, see toggles.md) with the same numbers.

## Motion
- Lines draw in over 600ms ease-out, each series 50ms after the last.
- Columns grow from the baseline and horizontal bars from the left, 400ms ease-out, 30ms apart.
- Run the draw-in on load and when switching back from Table. Never animate on every hover. Reduced motion means no draw-in.
