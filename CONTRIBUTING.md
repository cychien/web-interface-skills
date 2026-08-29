# Adding a principle

## The structure, and why it is this one

```
skills/web-interface/
├── SKILL.md              # index: always-rules + one trigger row per principle
└── principles/
    ├── _template.md
    └── <principle>.md    # the detail
```

One skill, not one skill per principle. This is a context decision, and it is the whole reason for the layout:

| Tier | What loads | When | Cost |
| --- | --- | --- | --- |
| 0 | the `description` in `SKILL.md` frontmatter | every session, always | ~60 tokens, fixed |
| 1 | the body of `SKILL.md` | only when the skill triggers | grows ~15 tokens per principle |
| 2 | one `principles/*.md` | only when the index points at it | paid only when relevant |

Every installed skill's description sits in context permanently. Splitting one hundred principles into one hundred skills would burn several thousand tokens on every unrelated task, forever. Folding them behind one description costs sixty, and the index behind it is only paid on UI work.

So the two things that must stay true:

1. **Tier 0 stays one description.** New principles never become new skills.
2. **Tier 1 stays scannable.** The index is a router, not a summary. One row, one line, phrased as the situation the reader is in.

## Steps

1. Copy `principles/_template.md` to `principles/<kebab-case-name>.md`.
2. Fill it in. The four sections are not optional: a rule without a *why* gets overridden, and a rule without a *checklist* cannot be reviewed against.
3. Add one row to the **Principles** table in `SKILL.md`. The "Read it when" column is the trigger, so write the situation ("a rounded element sits inside another rounded element"), not a restatement of the title ("nested border radius").
4. If the rule is one line, absolute, and applies to essentially every UI change, put it in **Always** instead of creating a file.

## Sizing rules

- **Too small for a file?** If a principle cannot justify roughly forty lines, it belongs in **Always**, or merged into a sibling. A file costs a read round-trip; make it worth one.
- **Index too long?** Past roughly one hundred rows, split the table into the group headings listed in `SKILL.md`. Past two hundred, promote each group to `principles/<group>/INDEX.md` and reduce `SKILL.md` to one row per group. Both are edits to the index, not migrations, which is why files stay flat until then.
- **Description drift.** The frontmatter `description` is the only always-on cost and the only trigger. Widen it when a new principle falls outside what it currently claims. Do not widen it to the point where it fires on non-UI work.

## What belongs here

- Rules with a defensible reason, ideally a derivation or a documented browser behaviour.
- Details that are cheap to get right while building and expensive to retrofit.
- Things that keep needing to be caught in review.

## What does not

- Taste preferences with no argument behind them.
- Anything already enforced by the linter, the type system, or the component library.
- Project-specific values. This repo holds the rule; a project's own config holds its numbers.
