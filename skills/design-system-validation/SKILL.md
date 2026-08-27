---
name: design-system-validation
description: Audits a wireframe screen element-by-element against @platform/design-system — replaces hand-rolled UI with shared primitives and semantic tokens (bg, border, shadow, dividers). Use when the user runs /design-system-validation, asks to validate design-system usage, check tokens/shadows/dividers, or complains that a screen is not using the shared design system.
---

# /design-system-validation — Design-System Fidelity Audit

Element-by-element audit of a live wireframe screen against
`@platform/design-system`. Complements [`verify`](../verify/SKILL.md) (spec
match) and [`design-system-components`](../design-system-components/SKILL.md)
(catalog): this skill **finds and fixes** hand-rolled UI and raw tokens.

Run when a designer points at a screen (or browser selection) and asks to align
it with the design system.

---

## Step 0 — Scope the screen

1. Identify the target: file path, route, browser selection, or tab name.
2. Read the screen source under `wireframes/<name>/src/…`.
3. Load the catalog: [design-system-components](../design-system-components/SKILL.md)
   (and `design-system/index.ts` / `design-system/components/ui/*` if unsure).

Do not redesign the screen. Only swap to design-system primitives/tokens (or
add a missing primitive).

---

## Step 1 — Inventory every visible element

Walk the screen top-to-bottom. For each interactive or visual piece, record:

| Element (what the user sees) | Current implementation | Design-system match |
|---|---|---|
| e.g. Search field | hand-rolled `<input>` + icon | `SearchInput` |
| e.g. Status pill | custom span | `Badge` |
| e.g. Analysis chips | custom span | `Tag` |
| e.g. Data table | custom `<table>` / bare divs | `DataGrid` / `Table` |
| e.g. Empty state | bordered div | `Card` (`flat` if dashed) |
| e.g. Page chrome bg | `bg-muted` / hex | `bg-background` |

Plain layout wrappers (`flex`, `grid`, spacing) may stay as `div`/`span`/`section`.

---

## Step 2 — Component checklist

Mark each ❌ if the screen hand-rolls something the catalog already provides:

| UI need | Prefer |
|---|---|
| Buttons, icon buttons | `Button` |
| Text / search fields | `Input` / `SearchInput` |
| Status / pill labels | `Badge` |
| Rectangular categorical chips (analysis types, etc.) | `Tag` (not `Badge` — pills are rounded-full) |
| Tables with sort/pager/selection | `DataGrid` |
| Bare table markup | `Table`, `TableHeader`, `TableBody`, `TableRow`, `TableHead`, `TableCell` |
| Menus / overflow actions | `DropdownMenu` (+ parts) |
| Dialogs / confirms | `Dialog` / `AlertDialog` |
| Selects / filters | `Select` / `Combobox` / `FilterBar` |
| Cards / empty states / elevated panels | `Card` (`flat` for hairline-only) |
| Tabs | `Tabs` (+ parts) |
| Dividers | `Separator` or token borders (`border-border`) |

**Missing primitive?** Add it to `design-system/components/ui/` (CVA + `cn()`,
semantic tokens, 3px radius), export from `design-system/index.ts`, then use it.
Do not leave a one-off copy in the wireframe.

---

## Step 3 — Token checklist

Reject hardcoded colors and ad-hoc elevation. Prefer:

| Concern | Use |
|---|---|
| Page / chrome background | `bg-background` |
| Raised surfaces (tables, cards, panels) | `bg-card` + `border-border` |
| Soft fills (table headers, chips) | `bg-muted` / `bg-secondary` |
| Text / borders | `text-foreground`, `text-muted-foreground`, `border-border`, `border-input` |
| Elevation | `shadow-elevation` (MB drop shadow from `--shadow`) — not raw `shadow-[…]` hex |
| Row / section dividers | `border-b border-border` / `border-t border-border` / `Separator` |
| Radius | token radius (`rounded-md` → 3px) — no one-off `rounded-[5px]` |

Never ship `bg-[#…]`, `text-[#…]`, `border-[#…]`, or inline hex shadows.

**Composed surfaces:** a `DataGrid` (or similar) on a muted/background page must
read as one elevated card — single outer shell with `bg-card`, `border-border`,
and `shadow-elevation`; avoid split borders between body and pager.

---

## Step 4 — Fix autonomously

For every ❌:

1. Replace with the catalog component, **or** create the primitive in
   `design-system/` if none exists.
2. Restyle with semantic tokens only.
3. Keep behavior and copy unchanged unless the catalog component requires a
   small API adaptation (e.g. `SearchInput` `onClear`).
4. Apply the same fix to sibling screens that share the broken pattern when the
   fix is in a shared primitive (`DataGrid`, `Card`, tokens).

---

## Step 5 — Typecheck

```bash
cd wireframes/<project-name>
npm run typecheck
```

Fix errors in touched files before reporting done.

---

## Step 6 — Report

Summarise with a before/after table (element → was → now). Call out any **new**
design-system primitives added. Do not claim pixel-perfect Figma match unless
[`verify`](../verify/SKILL.md) was also run.

---

## Common smells (from real audits)

- Hand-rolled search row (`div` + native `input` + `Search` icon) → `SearchInput`
- Gray analysis-type chips as custom spans → `Tag`
- Status as custom colored spans → `Badge` (via a thin domain wrapper is OK)
- Table without `bg-card` / elevation sitting on gray page chrome → fix
  `DataGrid`/container tokens
- Empty state as dashed `div` → `Card flat` with `border-dashed`
- Page body using `bg-muted` when it should be page chrome → `bg-background`
  (`bg-muted` is for soft fills inside components, e.g. header cells)

---

## Related skills

- Catalog / imports: [design-system-components](../design-system-components/SKILL.md)
- Spec-vs-build visual verify: [verify](../verify/SKILL.md)
- Building screens: [design](../design/SKILL.md)
