# Safe area

**Rule:** safe-area insets are a *minimum the device demands*, not spacing. Compose them as `max(design-spacing, inset)`, never `design-spacing + inset`, and apply them on the component that owns the edge.

## Why

`env(safe-area-inset-*)` is `0` on most screens and non-zero only where system UI intrudes. Adding it to your spacing makes every other device drift away from the design for no reason. `max()` keeps the inset invisible until it is actually needed. Additive is correct only when the design explicitly asks for clearance *beyond* the system UI.

## When it applies

Only when important UI can reach a viewport edge:

- edge-to-edge layouts, full-screen pages, app shells
- headers at the top edge; bottom nav, action bars, composers, footers at the bottom edge
- fixed or sticky edge controls
- full-width content in landscape, where the left/right insets are the non-zero ones
- PWAs and hybrid WebViews where content sits under system UI

A centered article or marketing page with generous margins usually needs none of this. Do not apply safe-area padding by default.

## Setup

```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

Without `viewport-fit=cover` every inset resolves to `0` and the rest of this page silently does nothing. Never disable zoom (`user-scalable=no`, `maximum-scale=1`) as a layout workaround.

Define the insets once, with platform-neutral names. Not `--notch-*`, `--iphone-*`, `--ios-*`:

```css
:root {
  --safe-top: env(safe-area-inset-top, 0px);
  --safe-right: env(safe-area-inset-right, 0px);
  --safe-bottom: env(safe-area-inset-bottom, 0px);
  --safe-left: env(safe-area-inset-left, 0px);
}
```

Always pass the `0px` fallback. Do not add `constant()` unless the project genuinely still supports iOS 11.0 to 11.2.

## Ownership

The component that touches an edge owns that edge's inset: header owns top, footer or composer owns bottom, edge-to-edge containers own left and right. Backgrounds own nothing and stay full-bleed.

```
┌────────────────────────────┐
│████████████████████████████│   background, blur, media: full-bleed
│██    text, controls     ███│   content: inside safe bounds
│████████████████████████████│
└────────────────────────────┘
```

Do not pad the page root with all four insets. That is correct only when the entire UI is deliberately confined to the safe rectangle, and it drags backgrounds and full-bleed media off the screen edges.

## Baseline

Responsive spacing and safe area answer different questions - what rhythm the design wants at this width, versus what the device requires - and `max()` combines them without double-padding.

```css
:root {
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

That is the whole default for a typical responsive site. Two things it depends on:

- **Physical properties, not logical ones.** Insets describe physical screen edges. `padding-inline: A B` maps to start/end, so in RTL it puts the left inset on the right edge. Use `padding-left` / `padding-right` for anything combined with an inset.
- **Safe area does not replace a width constraint.** `max-width` plus `margin-inline: auto` still does the centering; the insets only protect the mobile edges.

Breakpoint tokens instead of `clamp()` are equally valid. Pick whichever the design system already uses.

## Viewport height is a separate concern

`dvh` sizes a surface against the dynamic viewport and has nothing to do with insets. Use it only where a component genuinely fills the screen, never on ordinary long-form pages:

```css
.fullscreen {
  min-height: 100vh;
  min-height: 100dvh;
}
```

## Do not patch what is not broken

Order of preference: normal flow and responsive CSS, then `env()` insets, then `dvh`/`svh` when height is actually the problem, and only last a minimal runtime workaround.

**Keyboard: do nothing by default.** For ordinary forms, search, checkout, and settings, let the browser reveal the focused field and scroll it into view. Do not infer keyboard state from focus, do not attach `VisualViewport` listeners preemptively, and do not zero the bottom inset because an input has focus.

Add keyboard handling only after reproducing a user-visible failure: a gap between a bottom composer and the keyboard, a control covered or unusable, the UI left displaced after dismissal, flicker caused by a resize handler, or blank space the user can scroll into. Viewport numbers that merely look odd while the UI renders correctly are not a failure.

**No sniffing.** Do not branch on iOS version, device model, or browser brand. Fix reproduced behaviour, and prefer capability detection.

## Hybrid apps

In WKWebView, Android WebView, Capacitor, Cordova, or React Native WebView, pick one owner for system insets: native padding or web CSS, never both. Two layers applying the same inset is the most common cause of doubled bottom padding.

## Failure modes

- A primary button under the home indicator, where the gesture bar swallows the tap.
- Doubled bottom padding, because native and web both applied the inset, or a parent and a child both did.
- Spacing that looks cramped on a device with no insets, because the code used `spacing + inset`.
- A background stopping short of the screen edge, leaving a strip of page behind a supposedly full-bleed hero.
- Landscape content tucked into the notch cutout, because only top and bottom were handled.

## Review checklist

- [ ] Some important UI actually reaches a viewport edge. If not, none of this is needed.
- [ ] `viewport-fit=cover` present, zoom not disabled.
- [ ] Insets centralized as tokens with platform-neutral names.
- [ ] `max(design spacing, inset)`, not addition.
- [ ] Applied on the edge-owning component, not the page root.
- [ ] Backgrounds still reach the edges.
- [ ] Left and right insets handled for landscape.
- [ ] Physical padding properties used, so RTL does not swap the insets.
- [ ] `dvh` only on genuinely full-height surfaces.
- [ ] No keyboard or user-agent workaround without a reproduced, user-visible failure.
- [ ] Hybrid apps: exactly one layer owns the insets.

## Tailwind

If the project uses Tailwind CSS, read `safe-area/tailwind.md`.
