# 21 Grams

Agent skills that make AI-built products look and feel considered. Each **scale** covers one purpose, installs on its own, and works through the components and conventions your project already has.

## Scales

| Scale | What it does | Status | Docs |
|---|---|---|---|
| **ui** | Uplifts UI built by AI so it stops looking AI-generated: house style, icons, charts, toggles, UX and animation principles, design and typography hacks, unslop rules | Available | [README](skills/ui/README.md) · [Changelog](skills/ui/CHANGELOG.md) |
| **ux** | UX | Coming soon | |

## Install

**Any agent that supports skills** (Claude Code, Cursor, Codex and others). Pick the scale:

```bash
npx skills add ilbognov/21-grams --skill ui
```

**Claude Code plugin** (installs every scale; they show up as `21-grams:ui`, `21-grams:ux`…):

```
/plugin marketplace add ilbognov/21-grams
/plugin install 21-grams@21-grams
```

**Claude.ai:** zip a scale's folder (e.g. `skills/ui`) and upload it under *Settings → Capabilities → Skills*.

## Repo layout

```
.claude-plugin/plugin.json        the 21-grams plugin (all scales)
.claude-plugin/marketplace.json   the 21-grams marketplace
skills/<scale>/SKILL.md           one folder per scale: ui, ux, …
skills/<scale>/README.md          the scale's docs
skills/<scale>/CHANGELOG.md       the scale's history
```

Each scale keeps its own changelog. Release tags are named `<scale>@<version>`, e.g. `ui@3.0.0`.

## License

[MIT](LICENSE)
