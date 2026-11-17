# 21 Grams UI (`ui`)

The UI scale of [21 Grams](../../README.md). Uplifts UI built by AI so it stops looking AI-generated.

AI-built interfaces share the same tells: mixed icon styles, indigo-to-violet gradients, the same 16px radius on everything, cards inside cards, 300ms ease-in-out on every transition, grey-500 for every secondary line, emoji in headings, "Unlock the power of…". 21 Grams UI finds those, then applies a fixed set of design rules **through the components and tokens your project already has**. You don't get a new UI kit, a new dependency or a redesign, just the same product done with care.

It works with Claude Code and any agent that supports [Agent Skills](https://agentskills.io).

## Install

**Any agent that supports skills** (Claude Code, Cursor, Codex and others):

```bash
npx skills add ilbognov/21-grams --skill ui
```

**Claude Code plugin:**

```
/plugin marketplace add ilbognov/21-grams
/plugin install 21-grams@21-grams
```

**Claude.ai:** download this repo, zip the `skills/ui` folder, and upload it under *Settings → Capabilities → Skills*.

## Use

Ask your agent in plain words:

- "Uplift the dashboard with 21 grams UI"
- "Make this settings page less AI-looking"
- "Audit the checkout flow against the 20 UX principles"
- "Polish the charts and toggles on the analytics screen"

The skill takes an inventory of your design system, audits the screen, shows you the findings, applies the fixes in your own components (tokens first, then shared components, then screens), and verifies the result in the browser.

## Rule zero: your components, not ours

- Every fix goes into the project's existing tokens and components: the `Button` fix goes in `Button`, the colour fix goes in the token.
- It never adds a UI kit, icon set, chart or animation library to get an effect. It uses what's installed, or plain CSS.
- When something is genuinely missing (say, a segmented control), it builds it from your existing primitives and conventions, and tells you.
- Your brand stays yours. It changes how colours, fonts and icons are used, never what they are.

## What's inside

| Rule set | What it covers |
|---|---|
| **House style** (`rules/`) | Defaults for what your project hasn't decided: radius (12/8/4, nested), buttons, motion, type, spacing, colour, elevation, copy, plus icons, charts and toggles |
| **20 principles** (`references/principles.md`) | Disney's animation principles applied to UI, and the UX laws: Fitts, Hick, Miller, Doherty, Postel, Jakob, frequency of use |
| **10 design hacks** (`references/design-hacks.md`) | Concentric radius, alpha borders, OKLCH palettes and gradients, matched icon weight, masked edges, blurred icon swaps, dark-mode depth, `dvh`, multiply blending |
| **20 animation crafts** (`references/animation-craft.md`) | Popovers from the trigger at 0.95, exits 20% shorter, 30ms list stagger, 0.97 press, 1:1 drag, rubber-banding, shared-layout transitions |
| **20 unslop rules** (`references/unslop.md`) | Filler badges, redundant labels, random italics, decorative mono, show the real product, enlarge the main feature, specific headlines, one emphasised CTA, no glows, optical alignment, loading states |
| **10 typography hacks** (`references/typography.md`) | Reserved bold width, text-box trim, underline offset, superscript spacing, fluid display type, small-caps acronyms, curly quotes, middle truncation, auto hyphenation, line-clamped titles |

A few of the defaults:

- **Motion:** menus 220ms in and 175ms out, entrances ease-out and exits ease-in, no bounce on everyday UI, and frequent interactions are instant.
- **Buttons:** one primary per view; hover is a colour step only; press is a colour step plus `scale(.97)`; loading keeps the width.
- **Colour:** one accent, kept for actions, focus and selection. Status colours stay separate, and button text passes WCAG AA in every theme.
- **Icons:** one style, line, solid or duotone, never mixed in the same menu, nav or toolbar, not even for a selected state. One icon library, one stroke width.
- **Charts:** never the status colours as series colours, one scale per chart, direct labels, a crosshair tooltip, and a Chart / Table toggle.

## Credits

The principles, hacks, animation crafts and typography hacks are paraphrased and extended from five short-form design videos: *20 Principles of UX & Animation*, *10 Niche Design Hacks*, *20 Ways to Make Beautiful AI Animations*, *10 Niche Typography Hacks* and *20 Ways to Unslop AI Designs*. The house style was chosen by hand from side-by-side specimens.

## License

[MIT](../../LICENSE)
