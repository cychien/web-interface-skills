# Safe area

Modern OS and browser UI reserves space at the screen edges: status bar, notch, home indicator, gesture bar, address bar. A web interface respects that space and keeps its content and controls out of it.

Insets report how much is reserved on each edge. They are a minimum the device demands, not spacing, so compose with `max(spacing, inset)`, never `spacing + inset`.

## Baseline

Ship this on every page shell.

```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

```css
:root {
  --safe-top: env(safe-area-inset-top, 0px);
  --safe-right: env(safe-area-inset-right, 0px);
  --safe-bottom: env(safe-area-inset-bottom, 0px);
  --safe-left: env(safe-area-inset-left, 0px);

  --page-x: clamp(16px, 3vw, 32px);
  --page-y: clamp(12px, 2vw, 24px);
}

.header,
.container,
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

Use `padding-left` and `padding-right`, not `padding-inline`: insets are physical edges, and `padding-inline` swaps them in RTL.

## Placement

- The component that owns an edge owns that edge's inset: header top, footer or composer bottom, edge-to-edge containers left and right.
- Backgrounds, blur, and full-bleed media run to the screen edge and take no inset.
- Cards, buttons, list rows, and everything else inside the shell take no inset.
- Landscape moves the insets to left and right, so handle those wherever content runs full width.

## Do not add

- Keyboard handling. Let the browser scroll the focused field into view. Add `VisualViewport` logic only after reproducing a visible failure.
- Branches on iOS version, device model, or browser brand.
- `constant()`. `env()` with a `0px` fallback is enough.
- `user-scalable=no` or `maximum-scale=1`.
- `dvh` as part of safe area. It sizes the viewport; use `min-height: 100dvh` only where a surface fills the screen.
- A second inset owner in hybrid WebViews (Capacitor, Cordova, React Native WebView). Native or CSS, not both.

## Tailwind

Read `safe-area/tailwind.md`.
