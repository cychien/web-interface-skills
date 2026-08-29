# Safe area in Tailwind CSS

`../safe-area.md` is the source of truth. This only maps it onto utilities.

Copy `safe-area.css` into the project and import it after Tailwind:

```css
@import "tailwindcss";
@import "./safe-area.css";
```

Requires Tailwind v4, which is where `@utility` and `--value()` exist.

## API

Two concepts, padding only:

- `*-safe` - the raw device inset.
- `*-safe-or-<spacing>` - `max(inset, spacing)`. This is the one to reach for in normal product UI.

Both come in `p` `px` `py` `pt` `pr` `pb` `pl` forms.

| Utility | Resolves to |
| --- | --- |
| `pb-safe` | `padding-bottom: var(--safe-bottom)` |
| `pb-safe-or-4` | `padding-bottom: max(var(--safe-bottom), --spacing(4))` |
| `pb-safe-or-[18px]` | `padding-bottom: max(var(--safe-bottom), 18px)` |

Do not add `margin-safe`, positional, height, keyboard, or additive-offset utilities. If a layout seems to need one, re-read the ownership and keyboard sections of the principle first.

## Usage

```html
<header class="pt-safe-or-4 px-safe-or-4">…</header>
<main   class="px-safe-or-4 md:px-safe-or-6 lg:px-safe-or-8">…</main>
<footer class="pb-safe-or-4 px-safe-or-4 md:px-safe-or-6 lg:px-safe-or-8">…</footer>
```

Use the normal `md:` and `lg:` variants. Do not invent a separate safe-area breakpoint API.

Full-height surfaces use Tailwind's own `min-h-dvh`, which is a viewport-height concern and unrelated to safe area.

The `x` utilities set `padding-left` and `padding-right` rather than the logical `padding-inline` pair, so the insets stay on their physical edges in RTL.
