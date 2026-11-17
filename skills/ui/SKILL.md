---
name: ui
description: Uplift UI that was built by AI so it stops looking AI-generated and follows proven UX and motion principles, using the project's own components and tokens. Use when the user asks to uplift, polish, de-AI, refine or "make less AI-looking" an existing screen, component or frontend, asks for "21 grams UI" or "21 grams" (or "twenty-one grams"), or wants a UI audited against the house style, the 20 UX & animation principles (squash & stretch, anticipation, staging, easing, snappy timing, Fitts's, Hick's, Miller's, Doherty, Postel's, Jakob's law, frequency of use), the 10 design hacks (concentric radius, alpha borders, OKLCH, dvh and the rest) or the 20 animation crafts.
---

# 21 Grams UI

A pass over UI that already exists. 21 Grams UI (the UI package of the 21 Grams family) doesn't redesign the product and doesn't bring its own UI kit. It removes the tells of AI-built UI and applies a fixed set of rules **through the components and tokens the project already has**, so the result looks considered, feels fast and still belongs to the product.

## Rule zero: use the project's own components

Every change goes through what the project already uses. 21 Grams UI never builds a parallel set of components.

1. **Take an inventory before touching anything.** Note the design tokens or theme (CSS variables, Tailwind config, theme files), the component library (shadcn/ui, Radix, MUI, Chakra, an in-house kit, a client design system), the icon set, the chart library and the animation library. Record what each shared component is called and where it lives.
2. **Fix things where they live.** A button rule goes into the project's `Button` (a token, a variant, a prop or its styles), never into a one-off copy on a single screen. A colour or radius rule goes into the token, not into hard-coded values.
3. **Never add a component when one exists for the job,** and never add a dependency (UI kit, icon set, chart or animation library) to get a 21 Grams UI effect. Use what is installed. Without an animation library, use CSS transitions.
4. **When a piece is genuinely missing** (no segmented control, no switch), build it from the project's existing primitives and tokens, following its file layout and naming. Say so in the report.
5. **The house-style values are defaults for gaps only.** `rules/` and `tokens/tokens.css` give values for what the project hasn't decided. Map them onto the project's tokens. Never paste `tokens.css` alongside an existing system.
6. **Brand stays the project's.** Brand colours, fonts, logos, icon style and voice are never replaced. 21 Grams UI changes how they are used (contrast, hierarchy, spacing, motion), not what they are.

**Precedence:** the user's words, then the project's design system and brand, then the 21 Grams UI house style. The principles, hacks and animation crafts apply everywhere, expressed in the project's own components.

## What's inside

1. **House style.** Eight areas in `rules/`: `radius.md` (12/8/4 nested), `buttons.md` (36px, .97 press), `motion.md` (smooth, from the trigger, no bounce), `type.md` (tight, few sizes), `spacing.md` (grouped 4pt), `colour.md` (one accent, AA), `elevation.md` (tonal fills), `copy.md` (plain and helpful). Plus three component files: `icons.md` (one style, line, solid or duotone, never mixed), `charts.md` (line, column and horizontal bars) and `toggles.md` (switch and segmented control). Default values are in `tokens/tokens.css`.
2. **The 20 principles.** UX and animation principles in `references/principles.md`.
3. **The 10 design hacks.** CSS-level craft details in `references/design-hacks.md`.
4. **The 20 animation crafts.** Implementation-level motion rules (origins, durations, stagger, press, drag, shared layout) in `references/animation-craft.md`.
5. **The 10 typography hacks.** Reserved bold width, text-box trim, underline offset, superscript spacing, fluid display type, small-caps acronyms, curly quotes, middle truncation, auto hyphenation and line-clamped titles, in `references/typography.md`.
6. **The 20 unslop rules.** Composition and content tells (filler badges, redundant labels, random italics, decorative mono, abstract hero art, equal-weight features, vague headlines, glows, optical alignment, loading states) in `references/unslop.md`.

If a data-visualisation skill is installed, load it as well whenever a chart is involved.

## Workflow

1. **Take the inventory** (rule zero). If the project has no design system at all, say so and use the house-style defaults.
2. **Audit before changing anything.** Go through the screen or component and list findings grouped by area (radius … copy), principle number, hack number and craft number. Use the checklists at the end of `references/principles.md`, `references/design-hacks.md`, `references/animation-craft.md`, `references/typography.md`, `references/unslop.md` and `rules/icons.md`. Each finding gets the file and line, what is wrong, the fix, and **which existing component or token the fix goes into**. Flag every place where a 21 Grams UI rule conflicts with the project's design system, so the user can decide which wins.
3. **Show the audit to the user** as a short list and ask before applying broad changes. Small, obvious fixes in the requested scope can go straight in.
4. **Apply the fixes** in this order: tokens → shared components → screens. Keep diffs scoped to what was audited and in the project's own conventions (formatting, lint, naming).
5. **Verify in the browser.** Before and after screenshots of each changed screen. Check hover, press, focus, loading, error, both themes and reduced motion. Measure button and text contrast; don't eyeball it. For motion, record the before and after if possible. A before/after page with a draggable divider and working interactions on both sides is the clearest way to review an uplift.
6. **Report** what changed per area, principle, hack and craft, which components and tokens were touched, and anything left undone.

## House style at a glance (defaults for gaps)

- Radius 12 containers / 8 controls / 4 small parts, nested as outer − padding. No pills except tags and toggles.
- Buttons 36px (32 compact, 40 prominent), radius 8, 14/500, one solid primary, one primary per view, hover = colour step only, press = colour step + `scale(.97)` 150ms, loading keeps width.
- Motion: no bounce on everyday UI. Menus 220ms in / 175ms out from `scale(.95)` at the trigger, panels 240 / 190, entrances ease-out, exits ease-in (~80% of the entrance), list rows staggered 30ms, frequent interactions instant.
- Type: the project's fonts (Geist and Geist Mono when there are none), sizes 12/14/16/22/28, weights 400/500/600, headings −0.022em, at most four sizes per screen. On mobile, headings go up one step: section 18, card 16.
- Chat send on mobile is an icon-only 44×44 paper-plane button with `aria-label="Send"`.
- Spacing: 4pt scale. Tighter inside groups than between them (4 / 6 / 16 / 24–32 / 48). Select chevron 12px from the right, padding-right 36px.
- Colour: one accent (actions, focus, selection), status colours separate, **button text ≥ 4.5:1 in both themes** with `--on-accent` per theme.
- Elevation: resting surfaces are a fill step with no border or shadow. Only floating layers get a ring and shadow. Dark mode is lighter per layer.
- **Icons: one style per product, line, solid or duotone, and never mixed in a menu, nav, toolbar, list or card. Selected states change colour, not icon style. One icon library, one stroke width, one size per group.**
- Copy: verb + object buttons, errors with cause and fix, sentence case, no emoji, no hype words.

## Non-negotiables (from the 20 principles)

- User-triggered UI motion is 120–300ms, and exits are about 80% of the entrance. Never `linear` for movement.
- Easing matches the direction: enter ease-out, exit ease-in, A→B on screen ease-in-out. No overshoot on everyday UI.
- High-frequency interactions (keyboard nav, list highlight, tabs in tools) are instant.
- Every input is acknowledged in under 100ms. Use optimistic UI for saves. Show progress past 400ms.
- Hit areas are at least 44×44 on touch and 32×32 on dense desktop, even when the icon is smaller.
- One focus and one primary action per view. Dim the context when something takes focus.
- Long numbers are chunked. Inputs accept messy formats and echo back the clean value.
- Standard placement and icons unless there's a reason not to.
- Every component state is designed: idle, hover, pressed, loading, success, error, disabled.
- `prefers-reduced-motion`: remove movement, scale and overshoot, keep a brief opacity change.

## Non-negotiables (from the 10 hacks)

- Nested radius: inner = outer − padding.
- Borders are alpha (`rgb(0 0 0 / .12)`), never solid grey hex on varied surfaces.
- Palettes and gradients in OKLCH (`in oklch` on gradients).
- Icon stroke matches the weight of adjacent text.
- Horizontal scrollers fade at the edges with a mask.
- Icon swaps crossfade with `filter: blur(4px)`.
- Dark mode: each higher layer is lighter (page < card < menu).
- Mobile full-height: `dvh`/`svh`, never bare `100vh`.
- White-background product shots on tinted cards: `mix-blend-mode: multiply`.

## Non-negotiables (from the 10 typography hacks)

- Bold-on-hover or bold-on-select never shifts layout (reserve the bold width).
- Single-line labels in buttons and badges are optically centred (`text-box-trim`).
- Link underlines clear descenders (`text-underline-offset: 0.2em`). Superscripts don't break line rhythm.
- Real punctuation in copy: curly quotes, apostrophes, en dashes, `…`.
- Names that differ at the end are middle-truncated. Card titles in grids are clamped to the same line count.

## Non-negotiables (from the 20 animation crafts)

- Popovers and menus grow out of their trigger (`transform-origin` at the trigger), start at `scale(.95)`, never `scale(0)`, and exit back into the trigger.
- Old and new states overlap. There is never a blank frame between Save and Saved.
- Drags track the pointer 1:1 with no transition while held, and rubber-band past their bounds.
- Card → detail expands the same element (shared `layoutId` / view transition), never a disconnected replacement.
- Segmented controls and tabs reveal the active label with a mask that travels with the indicator.
- Moving knobs stretch about 12% (area-preserving). Success gets one pulse.

## AI tells to remove

Mixed icon styles (a solid house beside an outline folder, an outline icon that turns solid when selected), two icon libraries on one screen, emoji used as icons, "NEW" filler pills above headlines, eyebrows that repeat the heading, one random italic or mono word in a headline, glossy 3D orbs instead of the real product, rows of equal feature cards, "X, meet Y." headlines, glowing gradient borders, indigo-to-violet gradients, gradient text, coloured glow shadows, the same 16px radius on everything (inner radius equal to outer), pill buttons beside rounded inputs, hover scale-up on cards and buttons, 300ms ease-in-out on everything, fade-up on page load, uniform `p-6 gap-6`, cards inside cards, shadow plus border plus radius on every block, grey-500 for all secondary text, emoji in headings, and copy like "Unlock", "Supercharge", "Seamless" or "Oops!".

## Credits

The principles, hacks and animation crafts are paraphrased and extended from five short-form design videos: "20 Principles of UX & Animation", "10 Niche Design Hacks", "20 Ways to Make Beautiful AI Animations", "10 Niche Typography Hacks" and "20 Ways to Unslop AI Designs". See the README for credits.
