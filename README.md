# web-interface-skills

Design engineering principles for the web, as an agent skill.

## Why use it

A UI that works on your laptop is not a UI that holds up on a real device. Interfaces break in the places nobody opens during development: under the home indicator, in landscape with a notch, in RTL, inside a WebView, on a screen with no insets at all.

Each principle here turns one of those constraints into a rule an agent applies while it builds, instead of a bug someone finds afterwards. You get interfaces that stay robust across devices and stay comfortable for the people using them, without having to review for the same details every time.

## Install

Any agent that reads `SKILL.md` - Claude Code, Cursor, Codex:

```
npx degit cychien/web-interface-skills/skills/web-interface .claude/skills/web-interface
```

Swap the destination for wherever your tool keeps skills, or use `~/.claude/skills/web-interface` to install it globally.

As a Claude Code plugin, so it updates with `/plugin`:

```
/plugin marketplace add cychien/web-interface-skills
/plugin install web-interface@web-interface-skills
```

## Principles

| Principle | Covers |
| --- | --- |
| `safe-area` | Reserved OS and browser space at the screen edges: page shell baseline, inset ownership, landscape, RTL, Tailwind utilities |
