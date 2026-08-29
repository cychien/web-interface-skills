# web-interface

Design engineering principles for the web, written as plain markdown - the details that separate a working UI from a crafted one.

## Layout

```
skills/web-interface/
├── SKILL.md              # index: always-rules + one trigger row per principle
└── principles/*.md       # the detail, read on demand
```

Plain markdown throughout, readable by any agent or by a person. See `CONTRIBUTING.md` for how principles are added and why the structure is shaped this way.

## Use it in Claude Code

```
/plugin marketplace add cychien/web-interface
/plugin install web-interface@web-interface
```

## Use it anywhere else

Clone it and point your tool at `skills/web-interface/SKILL.md`, or symlink `skills/web-interface` into wherever that tool keeps its skills. `.claude-plugin/` is two JSON files that only Claude Code reads; no other tool sees them and no content depends on them.
