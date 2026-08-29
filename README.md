# web-interface-skills

Design engineering principles for the web, as an agent skill.

## Why use it

Well-crafted interfaces come from a small set of decisions made correctly and consistently. This skill hands your agent those decisions as rules it applies while it builds.

The result is UI that is robust across devices, browsers, and orientations, and that feels considered to the people using it - by default, on the first pass, without a review round.

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
