# web-interface-skills

Design engineering principles for the web, as an agent skill.

## Why use it

Well-crafted interfaces come from a small set of decisions made correctly and consistently. This skill hands your agent those decisions as rules it applies while it builds.

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
