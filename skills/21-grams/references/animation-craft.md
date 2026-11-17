# 20 ways to make AI animations beautiful

Adapted from the short video "20 Ways to Make Beautiful AI Animations" (credited in the README).
These are implementation-level motion rules, more specific than the 20 principles in `principles.md`. Each entry has the rule, the before/after from the video, the code, and what to flag in an audit.
Where an entry overlaps an earlier principle or hack, the cross-reference is noted.

---

### 1. Ease-out for entrances
**Rule:** Things entering use ease-out: fast start, gentle landing.
**Demo:** An Options dropdown at 250ms. Before: ease-in, so it starts slow and looks laggy. After: ease-out.
**Code:** `transition: opacity 200ms cubic-bezier(.2,0,0,1), transform 200ms cubic-bezier(.2,0,0,1);`
**Flag:** `ease-in` or `ease-in-out` on entrances. (Principle #6.)

### 2. Dropdowns at 150–250ms
**Rule:** Dropdowns and menus open in 150–250ms.
**Demo:** Before: 600ms, which drags. After: 200ms.
**Code:** `--dur-menu: 200ms;`
**Flag:** Menus or popovers over 250ms. (Principle #9.)

### 3. Stagger list rows by 30ms
**Rule:** When a list appears as part of an opening surface, rows follow each other 30ms apart.
**Demo:** A sidebar list (Overview, Activity, Members, Settings). Before: 200ms between rows, so the list feels slow to fill. After: 30ms between rows.
**Code:**
```css
.menu.is-open li { animation: row-in 180ms cubic-bezier(.2,0,0,1) both; animation-delay: calc(var(--i) * 30ms); }
@keyframes row-in { from { opacity: 0; transform: translateY(-4px); } }
```
Cap the stagger at about 6 rows (total delay ≤ 180ms). Rows after that appear with the last.
**Flag:** Staggers of 100ms+ per row. Staggers on page-load content or on lists the user scrolls or filters repeatedly (principle #20).

### 4. Scale to 0.97 on press
**Rule:** Buttons scale down slightly while pressed.
**Demo:** A "Save changes" button. Before: no press feedback. After: `scale(0.97)` over 150ms, then back on release.
**Code:**
```css
button { transition: transform 150ms cubic-bezier(.2,0,0,1); }
button:active:not(:disabled) { transform: scale(.97); }
```
**Flag:** Buttons with no pressed state (principle #17). Press scales deeper than .95.

### 5. Stretch moving knobs 12%
**Rule:** A knob that travels (a toggle thumb, a slider handle) stretches about 12% along the direction of travel while moving, preserving its area.
**Demo:** A toggle. Before: a rigid circle slides across. After: an area-preserving stretch mid-travel.
**Code:**
```css
.toggle-thumb { transition: transform 200ms cubic-bezier(.4,0,.2,1); }
.toggle:active .toggle-thumb { transform: scaleX(1.12) scaleY(.89); } /* 1.12 × .89 ≈ 1, area kept */
```
**Flag:** Rigid toggle thumbs. Stretch over about 15%. (Principle #1 squash & stretch.)

### 6. Stagger as details settle
**Rule:** Secondary parts land a beat after the main body.
**Demo:** A "New message" card with a "1" badge. Before: the badge stops rigidly in sync with the card. After: the badge trails by 50ms.
**Code:** child `transition-delay: 50ms` on badges, icons and secondary text.
**Flag:** Composite elements that move as one slab. (Principle #5 follow through.)

### 7. Arcs for object movement
**Rule:** Objects that travel from one place to another follow a curve.
**Demo:** A "File" chip moving from From to To. Before: a straight line. After: a 32px arc.
**Code:** animate x with `--ease-move` and y with a separate keyframe that lifts 32px mid-way, or use `offset-path: path(...)`.
**Flag:** Long straight-line travel. (Principle #7.)

### 8. Pulse to confirm success
**Rule:** A success state gets one pulse.
**Demo:** "Save changes" → "Saved". Before: the label only. After: the label plus a single pulse.
**Code:**
```css
.btn.is-success { animation: pulse 400ms cubic-bezier(.2,0,0,1); }
@keyframes pulse { 0% { box-shadow: 0 0 0 0 rgb(0 0 0 / .25); } 100% { box-shadow: 0 0 0 8px rgb(0 0 0 / 0); } }
```
One pulse, never a loop. **Flag:** Silent confirmations, or looping pulses. (Principle #8.)

### 9. Ease-in-out for moves
**Rule:** Anything moving from one on-screen position to another uses ease-in-out.
**Demo:** A "Move" chip across a track, 300ms. Before: linear. After: ease-in-out.
**Code:** `cubic-bezier(.4,0,.2,1)`.
**Flag:** `linear` on movement. (Principle #6.)

### 10. Start popovers at 0.95
**Rule:** Popovers and menus scale in from 0.95, not from 0.
**Demo:** Before: `scale(0) → 1`, which looks like it's coming out of a point. After: `scale(0.95) → 1`.
**Code:** `from { opacity: 0; transform: scale(.95); }`
**Flag:** `scale(0)` or `scale(.5)` entrances on UI surfaces.

### 11. Enter from the trigger
**Rule:** A popover grows out of the element that opened it.
**Demo:** An Options menu. Before: `transform-origin: center`. After: `transform-origin: top right`, at the button.
**Code:** `transform-origin: var(--radix-popover-content-transform-origin, top right);` (or compute it from the trigger's position).
**Flag:** Centre-origin menus and popovers.

### 12. Exit to the trigger
**Rule:** On close, it shrinks back into the trigger. It doesn't fade toward the centre.
**Demo:** Before: a centre-origin fade. After: it exits toward the Close/Options button.
**Code:** keep the same `transform-origin` on exit, scaling to .95 with opacity 0.
**Flag:** Exits that collapse to the centre or a different point than the entrance.

### 13. No bounce on everyday UI
**Rule:** No spring overshoot on routine transitions.
**Demo:** A "Project settings" panel. Before: an underdamped wobble. After: no overshoot.
**Code:** use `cubic-bezier(.2,0,0,1)`, or springs with damping ratio ≥ 1 (Framer Motion: `{ type: "spring", bounce: 0 }`, or `duration: .25, bounce: 0`).
**Flag:** Overshoot or wobble on dialogs, panels, menus or tabs. Bounce is reserved for rare, playful moments.

### 14. Don't tween while held
**Rule:** While the user is dragging, the element follows the pointer 1:1, with no easing lag.
**Demo:** A slider thumb. Before: the thumb tweens behind the pointer (a ghost shows the lag). After: direct pointer tracking.
**Code:** during drag set `transition: none` and write the position on every `pointermove`. Re-enable the transition only for the release or snap.
**Flag:** Sliders, sheets and draggables with CSS transitions active during drag.

### 15. Make exits 20% shorter
**Rule:** Exits are about 20% shorter than entrances.
**Demo:** An Open/Close menu. Before: 250ms in and 250ms out. After: 250ms in and 200ms out.
**Code:** `--dur-exit: calc(var(--dur-enter) * .8);`
**Flag:** Exits equal to or longer than entrances. (Principle #9.)

### 16. Overlap old & new states
**Rule:** The new state comes in while the old one leaves. There is no empty frame between them.
**Demo:** A Save → Saved button. Before: out, then a blank beat, then in. After: enter and exit overlap.
**Code:** run both at once (`AnimatePresence mode="popLayout"`, or `mode="sync"`, never `"wait"` for small swaps). In CSS, stack both states and crossfade.
**Flag:** `mode="wait"` or sequential out-then-in on labels, icons and tab content.

### 17. Masks for reveals & colour
**Rule:** Reveal content and change text colour with a clip or mask, not a fade.
**Demo:** A Notes/Files segmented control with content below. Before: the content fades and the text crossfades colour. After: the content is clipped in and the active text colour is revealed by a mask that moves with the pill.
**Code:**
```css
/* duplicate the labels in the active colour, clip them to the pill's rect */
.seg-active-layer { clip-path: inset(0 var(--right) 0 var(--left) round 8px); transition: clip-path 200ms cubic-bezier(.4,0,.2,1); }
```
**Flag:** Segmented controls and tabs whose label colour fades separately from the moving indicator.

### 18. Crossfade icons + blur
**Rule:** Swap icons with scale, opacity and blur together.
**Demo:** Copy → check. Before: a hard icon replacement. After: scale + opacity + blur.
**Code:** `.out { opacity: 0; transform: scale(.8); filter: blur(4px); }`, 150ms. (Same as hack #7.)

### 19. Rubber band past bounds
**Rule:** Dragging past a limit meets diminishing resistance and springs back on release. It doesn't hard-stop.
**Demo:** A "Drag" chip against a limit line. Before: a hard stop at the edge. After: diminishing resistance past the limit.
**Code:**
```js
const over = x - limit;
const dampened = over > 0 ? limit + over * 0.55 / (1 + over / 120) : x;
```
On release, animate back to the limit with `--ease-out` over about 250ms.
**Flag:** Sheets, carousels and drawers that clamp hard at their bounds.

### 20. Reuse the same layoutId
**Rule:** When an item expands into a detail view, animate the same object. Don't replace it with a disconnected new one.
**Demo:** A "Project brief" card. Before: a disconnected replacement appears. After: the same object expands into the panel.
**Code:** Framer Motion `<motion.div layoutId={\`project-${id}\`}>` on both the card and the expanded view. Without Framer Motion, use the View Transitions API with matching `view-transition-name`, or a FLIP transform.
**Flag:** Card → detail transitions that fade between two unrelated elements.

---

## Quick audit checklist

| # | Check | Pass when |
|---|---|---|
| 1 | Entrances | ease-out |
| 2 | Menus | 150–250ms |
| 3 | List open | rows 30ms apart, cap ~6 |
| 4 | Press | scale .97, 150ms |
| 5 | Toggle and slider knobs | ~12% area-preserving stretch in motion |
| 6 | Composite | details trail ~50ms |
| 7 | Travel | arcs |
| 8 | Success | one pulse |
| 9 | Moves | ease-in-out |
| 10 | Popover start | scale .95 |
| 11 | Popover origin | at the trigger |
| 12 | Popover exit | back into the trigger |
| 13 | Everyday UI | no overshoot |
| 14 | Drag | 1:1, no transition while held |
| 15 | Exit length | ~80% of the enter |
| 16 | State swaps | overlap, no blank beat |
| 17 | Segmented and tabs | clip or mask reveal |
| 18 | Icon swap | scale + opacity + blur |
| 19 | Drag bounds | rubber band |
| 20 | Card → detail | shared layoutId / view transition |
