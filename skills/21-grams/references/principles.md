# The 20 principles of UX and animation

Adapted from the short video "20 Principles of UX & Animation" (credited in the README).
Principles 1–12 are Disney's animation principles applied to interface motion. Principles 13–20 are UX laws.
Each entry has the rule, what the video's before/after demo showed, how to apply it in code, and what to flag in an audit.

Global motion budget that these principles share:
- UI transitions: 120–300ms. Micro-feedback (press, toggle) 100–160ms. Never above 400ms for something the user triggered.
- Exits run faster than entrances: about 80% of the enter duration (see `animation-craft.md` #15).
- Always honour `prefers-reduced-motion`: drop movement and scale, keep a short opacity change.

---

## Part 1: Animation principles

### 1. Squash & stretch
**Rule:** Things squash a little on impact so they feel like they have weight.
**Demo:** An icon drops into a dock. Before: it lands rigidly. After: it compresses on landing and springs back.
**Apply:** On landing or press, use a short scale keyframe: `scaleY .92 / scaleX 1.06`, then back to 1 over about 180ms. Keep the deformation at 4–8% and never distort text.
**Flag:** Rigid drops and docks, or the opposite: over-bouncy "jelly" with more than 10% deformation.

### 2. Anticipation (wind-up)
**Rule:** A small wind-up before a big move.
**Demo:** A paper-plane "send" icon. Before: it shoots off. After: it pulls back slightly, then launches.
**Apply:** Only for big, deliberate moves (send, launch, delete-swipe). Use a 60–100ms counter-move of 2–4px or scale .96, then the main move. Never use it on hover or on high-frequency actions (see #20).
**Flag:** Big exits with no preparation. Wind-ups on everyday controls.

### 3. Staging the focus
**Rule:** Direct the eye to one thing at a time.
**Demo:** A grid of cards. Before: everything stays equally loud when one card is selected. After: the selected card lifts forward and the rest dim and recede.
**Apply:** When something becomes the focus (modal, expanded card, popover), lower the context: dim to 40–60% opacity, a scrim, or a slight scale-down. Keep one primary action per view.
**Flag:** Several elements animating or highlighted at once. Modals with no scrim. Several primary buttons in one view.

### 4. Pose to pose
**Rule:** Set the key poses and let the rest fill in.
**Demo:** An element with a start pose, a key pose and an end pose on a 0–250–500ms timeline. The motion interpolates through the key pose.
**Apply:** Define states (closed / open / selected) as explicit tokens and let the transition interpolate between them. Use keyframes only when an intermediate pose matters. Animate `transform` and `opacity`, not layout properties.
**Flag:** Hand-tuned per-pixel animations. Animating `top`, `left`, `width` or `height` where `transform` would do.

### 5. Follow through
**Rule:** Parts keep moving after the main body stops.
**Demo:** A "Payment received $240.00" toast. Before: it stops as one block. After: the container lands and its contents settle a beat later.
**Apply:** Stagger children 30–60ms behind their container, or give the inner content a 2–4px overshoot that settles. Keep the total under 300ms.
**Flag:** Composite elements that move as one rigid slab. Staggers that run so long the content is late.

### 6. Slow in & slow out
**Rule:** Speed up and slow down, never constant.
**Demo:** A dot travelling a track. Before: linear, the same speed the whole way. After: slow, fast, slow.
**Apply:** Never `linear` for movement (only for spinners and progress). For moves from A to B on screen, use ease-in-out `cubic-bezier(.4,0,.2,1)`. Things entering use ease-out `cubic-bezier(.2,0,0,1)`. Things leaving use ease-in `cubic-bezier(.4,0,1,1)`.
**Flag:** `linear` on movement. One easing curve used for everything regardless of direction, which is the usual AI tell.

### 7. Moving in arcs
**Rule:** Move along curves, not straight lines.
**Demo:** Add-to-cart. Before: the item flies in a straight diagonal to the cart. After: it follows an arc and the cart badge ticks to 1.
**Apply:** For travel across the screen (add to cart, fly to folder), animate x and y on different easings (for example x ease-out, y ease-in), or use `offset-path`. Short in-place moves stay straight.
**Flag:** Long diagonal straight-line travel.

### 8. Secondary action
**Rule:** A small flourish that backs up the main action.
**Demo:** A Save button. Before: it just swaps to "✓ Saved". After: the check arrives with a small sparkle or ring burst.
**Apply:** Add one supporting detail to meaningful confirmations: a check that draws, a ring pulse, a count tick. Keep it under 400ms, and it must never block the next action.
**Flag:** Confirmations with no acknowledgement at all, or flourishes stacked on every click.

### 9. Snappy timing
**Rule:** Duration sets the feel. Keep UI motion under 300ms.
**Demo:** A notification-bell tooltip. Before: 500ms, which feels sluggish. After: 150ms.
**Apply:** Tooltips 120–150ms. Menus and popovers 150–250ms (house: 220ms). Panels, drawers and dialogs 200–280ms (house: 240ms). Page-level 250–300ms. Exits about 80% of the entrance.
**Flag:** Any user-triggered UI transition at 400ms or more. A blanket `duration-300` or `duration-500` everywhere.

### 10. Exaggerated feedback
**Rule:** Push it past real so the moment lands.
**Demo:** A login with the wrong password. Before: a subtle red message. After: the field shakes, its border goes red and the message appears.
**Apply:** Errors and key moments get one emphatic but brief cue: a horizontal shake (±6px, 3 cycles, about 300ms) on a rejected field, a bounce on a success. Pair it with text so the cue doesn't rely on motion alone.
**Flag:** Errors that only change a tiny line of text. Motion used as the only error signal.

### 11. Solid drawing in 3D
**Rule:** Give flat things depth and volume.
**Demo:** A credit card. Before: flat, with `perspective: none`. After: `perspective: 700px` with a slight tilt and a 3D flip to the back.
**Apply:** For objects meant to feel physical (cards, tickets, devices), set `perspective: 600–900px` on the parent, tilt by a few degrees, and use `backface-visibility: hidden` for flips. Ground it with a soft shadow that responds to the tilt.
**Flag:** Flips done as a 2D `scaleX` squash. 3D tilt applied to ordinary UI panels where it isn't meaningful.

### 12. Overall appeal
**Rule:** The sum of every detail, done with care.
**Demo:** Before: a grey "Downloading..." button that becomes a plain "Done". After: a circular progress icon that resolves into a solid "✓ Done" pill.
**Apply:** Every state of a component is designed: idle, hover, pressed, loading, success, error, disabled. The loading state keeps the button's width. The success state is distinct.
**Flag:** Default browser-looking states. A loading state that changes layout. Missing success or error states.

---

## Part 2: UX laws

### 13. Fitts's law
**Rule:** Bigger, closer targets are faster to hit.
**Demo:** Before: a tiny × far from the cursor, 450ms to hit. After: a large "Close" pill near the cursor, 330ms.
**Apply:** Put primary actions where the pointer or thumb already is. Make frequent targets larger. Use screen edges and corners for important controls on desktop.
**Flag:** Tiny icon-only close or confirm buttons. Primary actions placed far from the related content.

### 14. Bigger hit areas
**Rule:** The clickable zone can be bigger than it looks.
**Demo:** A heart icon. Before: a 24×24 hit area, so the tap misses. After: a 44×44 hit area around the same 24px icon.
**Apply:** Minimum hit target 44×44 (touch) and 32×32 (dense desktop), with the visual icon staying smaller. Extend it with padding or a `::before` inset of −10px. Keep adjacent targets from overlapping.
**Flag:** Icon buttons whose clickable box equals the glyph (16–24px).

### 15. Hick's law
**Rule:** More choices, slower decisions.
**Demo:** Before: 16 food options in a dense grid. After: 4 large options.
**Apply:** Show the few likely choices up front, then use progressive disclosure ("More…", search, grouping). Recommend a default.
**Flag:** Long flat option lists, menus with more than about 7 ungrouped items, and settings pages that show everything at once.

### 16. Miller's law
**Rule:** We hold about 7 things at once, so chunk it.
**Demo:** A raw card number `4532015112830366` and phone number `4155550132`. After: `4532 0151 1283 0366` and `415 555 0132`.
**Apply:** Format long numbers and codes in groups (cards 4-4-4-4, phones by locale, IBANs in 4s). Group form fields and navigation into sets of 5–9. Use `font-variant-numeric: tabular-nums` for numbers.
**Flag:** Unformatted long numbers and IDs. Navigation or forms with more than 9 ungrouped items.

### 17. Doherty threshold
**Rule:** Respond within 400ms or it feels slow.
**Demo:** A Save button. Before: a spinner for 817ms to 2,000ms. After: an instant "✓ Saved" at 100ms.
**Apply:** Acknowledge every input in under 100ms (pressed state). Use optimistic UI for likely-to-succeed actions and roll back on failure. If work takes more than 400ms, show progress or a skeleton. Never block on a spinner for something that could be optimistic.
**Flag:** Buttons with no pressed state. Spinners on fast actions. Saves that wait for the server before any visual change.

### 18. Postel's law
**Rule:** Accept messy input, give back clean output.
**Demo:** A date field with "15 j" typed. Before: strict, an error saying "Use the format YYYY-MM-DD". After: it parses to "Thursday, 15 January 2026" with a green check.
**Apply:** Parse loose formats for dates, phones, cards, currency, spaces and case. Echo back the normalised value so the user can confirm it. Validate on blur, not on every keystroke.
**Flag:** Format-policing error messages. Inputs that reject pasted values with spaces or dashes.

### 19. Jakob's law
**Rule:** People expect your app to work like the others.
**Demo:** A shop page. Before: the cart sits at the bottom-left and the logo at the top-right. After: the logo is top-left and the cart top-right.
**Apply:** Use the conventions for placement (logo top-left, account and cart top-right, search at the top), icons (gear = settings, magnifier = search) and patterns (⌘K palette, Esc closes, Enter submits).
**Flag:** Novel navigation or icon meanings with no payoff. Re-invented standard controls.

### 20. Frequency of use
**Rule:** The more it's used, the less it should animate.
**Demo:** A command palette navigated with ↑ and ↓. Before: the highlight animates on every step. After: it moves instantly.
**Apply:** High-frequency interactions (keyboard navigation, list selection, typing, tab switching in tools) are instant or 50–80ms with opacity only. Save expressive motion for rare moments: first run, success, errors.
**Flag:** Animated highlights in lists and palettes. Transitions on things the user does dozens of times a minute.

---

## Quick audit checklist

| # | Check | Pass when |
|---|---|---|
| 1 | Landings and drops | Small squash, 4–8% |
| 2 | Big launches | Short wind-up, never on frequent actions |
| 3 | Focus | One thing highlighted, context dimmed |
| 4 | States | Explicit state tokens, transform and opacity only |
| 5 | Composite motion | Children settle 30–60ms after the parent |
| 6 | Easing | No linear movement, easing matched to direction |
| 7 | Long travel | Arcs, not straight diagonals |
| 8 | Confirmations | One supporting flourish |
| 9 | Duration | 120–300ms, exits faster |
| 10 | Errors | Emphatic cue plus text |
| 11 | Physical objects | Real perspective for flips and tilts |
| 12 | Component states | All 7 states designed |
| 13 | Target placement | Primary near the pointer, large |
| 14 | Hit areas | 44×44 touch / 32×32 dense |
| 15 | Choices | ≤ 7 visible, the rest disclosed |
| 16 | Long numbers | Chunked, tabular-nums |
| 17 | Response | Pressed state < 100ms, optimistic saves |
| 18 | Inputs | Forgiving parse, normalised echo |
| 19 | Conventions | Standard placement and icons |
| 20 | Frequent actions | Instant, no decorative motion |
