# 21 Grams UI changelog

## 4.2.1 — 2026-11-17

- **Equal insets for nested controls** (`rules/layout.md`, `rules/toggles.md`): a control inside another (segmented options in their track, a button in an input, chips in a field) has the same gap on all four sides. Inner height = outer height − 2 × padding, the outer control keeps its neighbours' height, and the audit measures every side. New AI tell for uneven inner padding.

## 4.2.0 — 2026-11-17

Six rules learned from reviewing a real uplift pass.

- **New `rules/layout.md`.**
  - Table-like lists of gapped row cards become one container with 1px hairline dividers; only the container is rounded, hover and selection are fills. Card grids stay cards.
  - Screen actions are one group at the right of the screen's header, secondary first and the solid primary in the corner, never mixed into date pickers or filters; duplicates below are removed.
  - When a product shows a placeholder instead of a logo (initials tile), the audit asks the user for their logo; the supplied lockup is used as is.
- **Segmented controls** (`rules/toggles.md`): no outline. The track is filled with the soft border colour (about 9% ink) and the selected option is raised; in dark mode the track sinks and the selection rises. Unselected labels must pass 4.5:1 on the track.
- **Chart hover** (`rules/charts.md`): stacked or segmented marks open a breakdown panel (one row per segment, hovered row highlighted, flips near the edge) instead of a native `title` tooltip.
- **Copy** (`rules/copy.md`): no version tags, draft names or internal shorthand on screen, and one form of address throughout.
- New AI tells for each in SKILL.md.

## 4.1.0 — 2026-11-17

- **Mono is for code only (strict).** Monospace is now limited to code, commands and copyable hashes or keys. Labels, eyebrows, badges, tags, buttons, table headers, timestamps, IDs and numbers use the UI sans, with `tabular-nums` for aligned figures. Fixes `rules/type.md`, which had sent numbers, IDs and timestamps to Geist Mono and allowed small uppercase mono labels. Added an audit search and new AI tells.

## 4.0.0 — 2026-11-17

- The family is now `21grams`, without the hyphen: the repo is `ilbognov/21grams`, the plugin and marketplace are `21grams`, and the skill appears as `21grams:ui` in Claude Code.
- Install: `npx skills add ilbognov/21grams --skill ui`, or `/plugin marketplace add ilbognov/21grams` then `/plugin install 21grams@21grams`. Old `21-grams` links redirect on GitHub.

## 3.0.0 — 2026-11-17

- Shorter names: the skill is now `ui` (`npx skills add ilbognov/21-grams --skill ui`). In Claude Code, one `21-grams` plugin holds every scale, so this one appears as `21-grams:ui`.
- Layout: `skills/ui/` holds the skill, README and changelog. Tags are `ui@<version>`.

## 2.0.0 — 2026-11-17

- **Renamed to 21 Grams UI** (`21-grams-ui`). The repo is now the home of the 21 Grams family; a UX package will follow.
- New layout: `plugins/21-grams-ui/` holds the plugin, its skill, README and changelog. The repo root is the index of all scales; the Claude Code marketplace is still `21-grams`.
- Release tags are now per scale: `21-grams-ui@2.0.0`. Earlier tags `v1.0.0`–`v1.3.0` belong to this scale.
- Install changes: `npx skills add ilbognov/21-grams --skill 21-grams-ui`, or `/plugin install 21-grams-ui@21-grams`.

## 1.3.0 — 2026-11-17

- New `references/unslop.md`: 20 composition and content rules for unslopping AI designs, cross-referenced to the existing rules where they overlap.
- More AI tells in SKILL.md: filler badges, redundant eyebrows, random italic or mono words, abstract hero art, equal-weight feature grids, vague headlines, glowing borders, emoji icons.

## 1.2.0 — 2026-11-17

- New `references/typography.md`: 10 typography hacks (reserved bold width, text-box trim, underline offset, superscript spacing, fluid display type, small-caps acronyms, curly quotes, middle truncation, auto hyphenation, line-clamped titles), each with code and audit checks.
- `rules/type.md`: fluid `clamp()` allowed for display headings only; UI text stays on the fixed scale.

## 1.1.0 — 2026-11-17

- New `rules/icons.md`: one icon style (line, solid or duotone), never mixed within a menu, nav, toolbar, list or card, and unchanged across states. One library, one stroke width, one size per group.

## 1.0.1 — 2026-11-17

- Replaced project-specific examples in the type, chart and toggle rules with neutral ones.

## 1.0.0 — 2026-11-17

First public release.

- Rule zero: every fix goes through the project's own components and tokens; no new UI kits or dependencies.
- House style across eight areas (radius, buttons, motion, type, spacing, colour, elevation, copy) plus charts and toggles.
- 20 UX & animation principles, 10 design hacks and 20 animation crafts, each with apply and audit notes.
- Workflow: inventory → audit → approve → tokens → components → screens → verify → report.
