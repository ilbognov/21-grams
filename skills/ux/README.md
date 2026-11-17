# 21 Grams UX (`ux`)

The UX scale of [21 Grams](../../README.md). Audits and fixes the flows and usability of products built by AI.

AI-built products often look finished and still fail the people using them: a list with no empty state, a save that fails silently, a delete with no way back, a form that loses everything on one bad field, a flow with three steps that could be one. 21 Grams UX walks the real flows, finds those, and fixes them **through the components and patterns your project already has**.

> **Status: draft.** The structure is in place; the rule set is being written.

## Install

**Any agent that supports skills** (Claude Code, Cursor, Codex and others):

```bash
npx skills add ilbognov/21grams --skill ux
```

**Claude Code plugin:**

```
/plugin marketplace add ilbognov/21grams
/plugin install 21grams@21grams
```

## Use

- "Run 21 grams UX on the onboarding flow"
- "Audit the checkout for usability"
- "Fix the empty, loading and error states on the projects list"

## What it checks

The core UX laws (Hick's, Fitts's, Jakob's, Miller's, Doherty Threshold, Tesler's, Postel's) and a set of concrete UX rules, organised by area.

## Areas

Navigation, forms, states (empty, loading, error, success), feedback, onboarding, destructive actions and recovery, accessibility and keyboard, flows and task length, choice and cognitive load.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).
