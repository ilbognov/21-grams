# 2g · Buttons: ink, 36px

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

## Anatomy
| Property | Value |
|---|---|
| Height | 36px default · 32px compact (tables, toolbars) · 40px prominent (forms, empty states) |
| Padding x | 14px (12px compact, 16px prominent) |
| Radius | 8px |
| Type | 14px / 500 (13px compact) |
| Icon | 16px, left of label, gap 6px, stroke matched to the text (hack #5) |
| Icon-only | square at the button height, hit area ≥ 44×44 on touch (principle #14) |

## Icon-only send in chat
On mobile, the send button of a chat or ask-style input is **icon-only**: a 44×44 square, a paper-plane icon at 18px, radius 8, with `aria-label="Send"`. The label follows the state ("Sending", "Sent"). The states swap icon-to-icon (plane → spinner → check) with the blurred crossfade, and Sent gets one pulse. On desktop the button keeps its text label ("Ask", "Send").

```html
<button type="submit" class="send" aria-label="Send"><svg aria-hidden="true">…paper-plane…</svg></button>
```

## Variants
- **Primary:** ink fill (`--ink`), page-colour text. **One per view** (principle #3).
- **Secondary:** 7% ink fill, ink text. No border.
- **Ghost:** transparent, `--ink-2` text, 6% ink fill on hover.
- **Destructive:** ghost or secondary with `--err` text. It becomes a solid red fill only in the final confirm step.
- **Accent primary:** allowed only where the brand needs the main CTA in colour. The text must pass AA (see colour.md).

## States
| State | Treatment |
|---|---|
| Hover | colour step only (ink mixed 14% toward page). **No movement, no scale, no shadow.** |
| Pressed | colour step 24% **plus `scale(.97)` over 150ms** `--ease-out`, starting in < 100ms (principle #17, craft #4). Not applied when disabled. |
| Focus | 2px ring in `--accent`, 2px offset, `:focus-visible` only |
| Disabled | 40% opacity, `cursor: not-allowed`, no hover change |
| Loading | spinner 14px left of the label, label stays, **width does not change** |
| Success (after save) | label swaps to "✓ Saved" with a blurred icon swap (hack #7), then reverts after ~1.5s |

Transitions: `background-color 120ms cubic-bezier(.2,0,0,1), transform 150ms cubic-bezier(.2,0,0,1)`.

```css
button:active:not(:disabled) { transform: scale(.97); }
```

## Never
Gradients, glow shadows, hover scale or lift, press scale deeper than .95, emoji in labels, mismatched heights in one row, more than one primary in a view, labels like "Get started" or "Submit" (see copy.md).
