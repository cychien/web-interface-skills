# web-interface-skills

Design engineering principles for the web - the details that separate a working UI from a crafted one.

Installs as the `web-interface` skill.

```
/plugin marketplace add cychien/web-interface-skills
/plugin install web-interface@web-interface-skills
```

## Layout

```
skills/web-interface/
├── SKILL.md          # index: always-rules + one trigger row per principle
└── principles/*.md   # the detail, read on demand
```

One skill, not one per principle: only the frontmatter `description` stays in context permanently, so everything else is paid for only when it is actually relevant.
