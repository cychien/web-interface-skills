# web-interface-skills

Design engineering principles for the web, as an agent skill.

## Why use it

A UI that works on your laptop is not a UI that holds up on a real device. Interfaces break in the places nobody opens during development: under the home indicator, in landscape with a notch, in RTL, inside a WebView, on a screen with no insets at all.

Each principle here turns one of those constraints into a rule an agent applies while it builds, instead of a bug someone finds afterwards. You get interfaces that stay robust across devices and stay comfortable for the people using them, without having to review for the same details every time.

## Install

```
npx skills add cychien/web-interface-skills
```

Installs into whichever agents it detects - Claude Code, Cursor, Codex, and others. Add `-g` for user-level instead of project-level, or `-a '*'` to install for every agent it finds.

Claude Code can also take it as a plugin, which keeps it updated through `/plugin`:

```
/plugin marketplace add cychien/web-interface-skills
/plugin install web-interface@web-interface-skills
```

## Principles

| Principle | Covers |
| --- | --- |
| `safe-area` | Reserved OS and browser space at the screen edges: page shell baseline, inset ownership, landscape, RTL, Tailwind utilities |
