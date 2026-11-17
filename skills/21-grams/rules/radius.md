# 1g · Radius: nested 12 / 8 / 4

House default. When the project has its own system, express this through its components and tokens (SKILL.md, rule zero).

| Element | Radius |
|---|---|
| Containers (cards, panels, modals, popovers) | 12px |
| Controls (buttons, inputs, selects, segmented controls) | 8px |
| Small parts (chips, tags, badges, kbd, checkboxes) | 4px |
| Menu items inside a menu | 8px (menu 12 − menu padding 4) |
| Avatars, status dots, toggles' thumbs | fully round |

**Nesting:** inner = outer − padding (hack #1). A 12px card with 8px padding gets a 4px inset image. With 4px padding the inner part gets 8px. Compute it, never copy the outer radius down.

```css
.card  { border-radius: var(--r-container); padding: var(--pad); }
.inset { border-radius: max(0px, calc(var(--r-container) - var(--pad))); }
```

**Never:**
- Pill-shaped (`rounded-full`) buttons or inputs. Pills are only for tags and toggles.
- `rounded-2xl` / 16px+ on product UI containers.
- The same radius on a container and its inset child.
- Mixing radius systems in one view (a 12px card next to a 20px card).

**Tailwind mapping:** `rounded-xl` → 12px containers, `rounded-lg` → 8px controls, `rounded` → 4px small parts. Set these in the theme so `rounded-2xl` and `rounded-3xl` aren't used.
