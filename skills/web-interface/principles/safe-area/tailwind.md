# Safe area in Tailwind

Copy `safe-area.css` into the project and import it after Tailwind. Requires v4.

```css
@import "tailwindcss";
@import "./safe-area.css";
```

Use `*-safe-or-<spacing>` for product UI; `*-safe` gives the raw inset. Both come in `p` `px` `py` `pt` `pr` `pb` `pl` forms.

| Utility | Resolves to |
| --- | --- |
| `pb-safe` | `padding-bottom: var(--safe-bottom)` |
| `pb-safe-or-4` | `padding-bottom: max(var(--safe-bottom), --spacing(4))` |
| `pb-safe-or-[18px]` | `padding-bottom: max(var(--safe-bottom), 18px)` |

```html
<header class="pt-safe-or-4 px-safe-or-4">…</header>
<main   class="px-safe-or-4 md:px-safe-or-6 lg:px-safe-or-8">…</main>
<footer class="pb-safe-or-4 px-safe-or-4 md:px-safe-or-6 lg:px-safe-or-8">…</footer>
```

Normal `md:` and `lg:` variants apply. Full-height surfaces use `min-h-dvh`, which is unrelated to safe area.
