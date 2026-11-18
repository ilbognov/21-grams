# Tables: aligned, quiet, sortable

House default. Use the project's table component (or its data-grid library) and apply these through its props and styles (SKILL.md, rule zero). For lists of rows drawn as separate cards, see `layout.md`.

## Alignment
- **Text left, numbers right.** Amounts, counts, percentages and durations are right-aligned in the sans with `tabular-nums`, so digits line up. The header aligns with its column.
- **Nothing centred** except a column of icons or checkboxes, and **heatmap or score cells**, which read as tiles and may be centred.
- Units and currency appear in the header ("Amount, £") or consistently in every cell, never mixed.

## Look
| Part | Spec |
|---|---|
| Rows | split by a 1px alpha hairline. **No zebra stripes**, no borders between columns |
| Surface | the table sits on the card or page surface (white in light mode), not on a grey panel |
| Header | **the same size as the cells** (14), told apart by weight (500) and the secondary ink, sentence case, on the table's own surface. **No gradient, colour band or uppercase mono** |
| Cells | 14/400, row height 44px (36 compact), 12–16px horizontal padding |
| Empty cells | "N/A" (or an en dash) in the muted ink, never "No data" or a blank |
| Status | a small tinted tag, the **same width for every status** in the column, colour plus text (never colour alone), no emoji. Status colours stay separate from the brand accent |
| Long text | middle-truncate names that differ at the end; full value in a tooltip |

## Interaction
- **Headers that look clickable must sort.** Click sorts the column, click again reverses it. The sorted header shows a **simple line caret** (up or down, the product's icon style), never filled triangles or a double-arrow stack, and `aria-sort`. Never style headers as buttons if they do nothing.
- **Sensible first direction:** amounts and dates sort largest or newest first; statuses sort the most urgent first (Overdue before Paid).
- **Row hover is a slight fill tint** when rows are clickable. No flashes, gradients, lifts or shadows. Rows that do nothing on click get no hover.
- Clickable rows are links or buttons (keyboard reachable), with the focus ring inside the row.
- Sorting is instant; no row animation on re-order.

## Never
Zebra stripes with hairlines, a smaller header than the cells, "No data" in cells, filled sort triangles, gradient headers, everything centred, emoji statuses, status pills of different widths, numbers left-aligned or in mono, headers that look sortable but aren't, hover effects that flash or lift.
