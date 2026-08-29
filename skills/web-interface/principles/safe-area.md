# Safe area

Modern OS and browser UI reserves space at the screen edges: status bar, notch, home indicator, gesture bar, address bar. Keep content and controls out of it.

Insets report how much each edge reserves. They are a minimum, not spacing: compose with `max(spacing, inset)`, never `spacing + inset`.

## Baseline

Ship this on every page shell.

```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

```css
:root {
  --page-x: 16px;
  --page-y: 16px;

  --safe-top: env(safe-area-inset-top, 0px);
  --safe-right: env(safe-area-inset-right, 0px);
  --safe-bottom: env(safe-area-inset-bottom, 0px);
  --safe-left: env(safe-area-inset-left, 0px);
}

@media (min-width: 768px) {
  :root {
    --page-x: 24px;
    --page-y: 20px;
  }
}

@media (min-width: 1280px) {
  :root {
    --page-x: 32px;
    --page-y: 24px;
  }
}

.header,
.main,
.footer {
  padding-left: max(var(--page-x), var(--safe-left));
  padding-right: max(var(--page-x), var(--safe-right));
}

.header { padding-top: max(var(--page-y), var(--safe-top)); }
.footer { padding-bottom: max(var(--page-y), var(--safe-bottom)); }

.container {
  width: 100%;
  max-width: 1200px;
  margin-inline: auto;
}
```

Use the project's own spacing scale and breakpoints where it has them.

Use `padding-left` and `padding-right`, not `padding-inline`: insets are physical edges, and `padding-inline` swaps them in RTL.

## Placement

- The component touching an edge owns that inset: header top, footer or composer bottom, edge-to-edge containers left and right.
- Backgrounds and full-bleed media run to the edge, no inset.
- Nothing inside the shell takes an inset.
- Landscape moves insets to left and right: handle those wherever content runs full width.

## Implement with Tailwind

If the project uses Tailwind, `safe-area/tailwind.md` replaces the CSS above. Read it first.
