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
├── SKILL.md              # router: one trigger row per principle
└── principles/
    ├── safe-area.md      # the principle
    └── safe-area/        # sidecar assets, read only when relevant
        ├── tailwind.md
        └── safe-area.css
```

One skill, not one per principle. Only the frontmatter `description` stays in context permanently; the router is paid for once the skill triggers, and a principle file only when the router points at it.

Two rules follow from that:

- **`SKILL.md` is a router, not a document.** Nothing goes in it that does not change what an agent reads next. Notes for whoever edits the repo belong here in the README instead.
- **Keep it flat until it hurts.** Past ~100 rows, split the table under headings (layout and space, shape and depth, type and rhythm, states and interaction, motion, responsiveness and device, content and copy). Past ~200, promote each group to its own index and reduce `SKILL.md` to one row per group. Both are edits to the router, not file migrations.

Each principle follows the same shape: **Rule → Why → When it applies → How → Failure modes → Review checklist.**
