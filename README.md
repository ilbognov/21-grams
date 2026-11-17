# 21 Grams

Agent skills that make AI-built products look and feel considered. Each **scale** covers one purpose, installs on its own, and works through the components and conventions your project already has.

## Scales

| Scale | What it does | Status | Docs |
|---|---|---|---|
| **21 Grams UI** (`21-grams-ui`) | Uplifts UI built by AI so it stops looking AI-generated: house style, icons, charts, toggles, UX and animation principles, design and typography hacks, unslop rules | Available | [README](plugins/21-grams-ui/README.md) · [Changelog](plugins/21-grams-ui/CHANGELOG.md) |
| **21 Grams UX** (`21-grams-ux`) | UX | Coming soon | |

## Install

**Any agent that supports skills** (Claude Code, Cursor, Codex and others). Pick the scale:

```bash
npx skills add ilbognov/21-grams --skill 21-grams-ui
```

**Claude Code:** add the marketplace once, then install the scales you want:

```
/plugin marketplace add ilbognov/21-grams
/plugin install 21-grams-ui@21-grams
```

**Claude.ai:** zip a scale's skill folder (e.g. `plugins/21-grams-ui/skills/21-grams-ui`) and upload it under *Settings → Capabilities → Skills*.

## Repo layout

```
.claude-plugin/marketplace.json     one marketplace listing every scale
plugins/<scale>/
  .claude-plugin/plugin.json        the scale's plugin manifest and version
  skills/<scale>/SKILL.md           the skill itself (plus rules/, references/…)
  README.md · CHANGELOG.md          the scale's own docs and history
```

Each scale is versioned on its own. Release tags are named `<scale>@<version>`, e.g. `21-grams-ui@2.0.0`.

## License

[MIT](LICENSE)
