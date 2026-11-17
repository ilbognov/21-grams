# 21 Grams UI changelog

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
