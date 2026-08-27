---
name: design-system-components
description: Catalog of the local @platform/design-system component library (imports, variants, tokens, and Figma-to-code mappings). Use when building wireframe screens, importing components, or translating a Figma design/screenshot into code. Read reference.md for where to find per-component prop details.
---

# @platform/design-system — Component Catalog

## Golden rule: design-system components first

Before building any UI element, check this catalog for a matching component and
use it. **Never hand-roll a button, input, card, dialog, badge, tabs, tooltip,
menu, popover, etc. when the design system already provides one.** Plain
`div`/`span`/`section` are only for layout (flex, grid, spacing, positioning).

Unlike design-kit (which imports a prebuilt npm package), this kit **owns** its
design system as source under `design-system/`. So there are two moves, in order:

1. **Compose** existing primitives from `@platform/design-system`.
2. If a primitive genuinely does not exist, **add it** to
   `design-system/components/ui/` in the same shadcn + token style (CVA +
   `cn()`, semantic tokens, 3px radius), then export it from
   `design-system/index.ts`. Do not pull in a third-party UI kit.

See the golden rules in [AGENTS.md](../../../AGENTS.md).

## Import paths

```ts
// Components + the cn() helper — the barrel:
import { Button, Input, Card, Badge, cn } from "@platform/design-system";

// App chrome (layout) also comes from the barrel:
import { AppShell, AppSidebar, AppTopbar } from "@platform/design-system";

// Icons: lucide-react directly (already a dependency):
import { Search, ChevronDown, X, Plus } from "lucide-react";

// Deep import anything not on the barrel (the `@` alias → design-system root):
import { Button } from "@platform/design-system/components/ui/button";
```

Tokens are imported once in each app's `src/index.css`
(`@import "@platform/design-system/tokens";`) — never import them again in
components.

## Quick reference — UI primitives (`design-system/components/ui/*`)

| Component | Import name(s) | Notes |
|-----------|----------------|-------|
| Button | `Button`, `buttonVariants` | `variant`: default/secondary/neutral/destructive/outline/ghost/link · `size`: default/sm/lg/xs/icon |
| Badge / pill | `Badge`, `badgeVariants` | roles: default/secondary/destructive/success/warning/outline + MB vocab (valid/error/info/new/resolved/manual/normal/sparkle…) |
| Alert | `Alert`, `AlertTitle`, `AlertDescription` | `variant`: info/success/warning/error |
| Input | `Input`, `SearchInput` | `SearchInput` adds a leading icon + clear button |
| Textarea | `Textarea`, `NumberedTextarea` | flat MB field styling |
| Checkbox | `Checkbox` | Radix checkbox |
| Switch | `Switch` | Radix switch |
| Select | `Select`, `SelectTrigger`, `SelectContent`, `SelectItem`, `SelectValue`, `SelectGroup`, `SelectLabel`, `SelectSeparator` | 40px trigger |
| Combobox | `Combobox` | searchable single-select |
| DropdownMenu | `DropdownMenu`, `DropdownMenuTrigger`, `DropdownMenuContent`, `DropdownMenuItem`, `DropdownMenuCheckboxItem`, `DropdownMenuLabel`, `DropdownMenuSeparator`, … | |
| ToggleGroup | `ToggleGroup`, `ToggleGroupItem` | segmented control |
| Tabs | `Tabs`, `TabsList`, `TabsTrigger`, `TabsContent` | underline / pill / nav variants |
| Card | `Card`, `CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, `CardFooter` | |
| Dialog | `Dialog`, `DialogTrigger`, `DialogContent`, `DialogHeader`, `DialogTitle`, `DialogDescription`, `DialogFooter`, `DialogClose` | |
| Drawer | `Drawer`, `DrawerContent`, `DrawerHeader`, `DrawerTitle`, `DrawerDescription`, … | side sheet |
| Tooltip | `Tooltip`, `TooltipTrigger`, `TooltipContent`, `TooltipProvider` | white MB tooltip; provider is in each app's `main.tsx` |
| Popover | `Popover`, `PopoverTrigger`, `PopoverContent`, `PopoverAnchor` | |
| Avatar | `Avatar` | initials from `name` |
| Breadcrumb | `Breadcrumb`, `BreadcrumbList`, `BreadcrumbItem`, `BreadcrumbLink`, `BreadcrumbPage`, `BreadcrumbSeparator` | |
| Table | `Table`, `TableHeader`, `TableBody`, `TableRow`, `TableHead`, `TableCell` | MB header styling |
| Tag | `Tag`, `tagVariants` | Rectangular categorical chips (analysis types); not a status pill |
| DataGrid | `DataGrid` | TanStack-table data grid |
| Progress | `Progress` | `tone`: default/success/warning/destructive |
| Slider | `Slider` | |
| Separator | `Separator` | |
| Skeleton | `Skeleton` | loading placeholder |
| Spinner | `Spinner`, `spinnerVariants` | |
| ScrollArea | `ScrollArea`, `ScrollBar` | |
| Label | `Label` | |
| Toast | `Toaster`, `useToast`, `toast` (`toast.tsx` primitives) | add `<Toaster />` once per app |
| ButtonSplit | `ButtonSplit` | primary + dropdown split button |
| DatePicker | `DatePicker`, `DateRangePicker`, `PresetsDatePicker` | |

## Quick reference — MindBridge-specific primitives

| Component | Import | Use for |
|-----------|--------|---------|
| `RiskCard` | `RiskCard` | Risk summary card (uses risk tokens) |
| `StatusDot` | `StatusDot` | Small status indicator dot |
| `Stepper` | `Stepper` (`Step` type) | Multi-step progress header (used by `WizardShell` block) |
| `Facet` | `Facet` | Collapsible checkbox-filter group with counts |
| `FilterBar` | `FilterBar` (`ActiveFilter`, `SortOption` types) | Removable filter chips + sort dropdown |

## App chrome (`design-system/components/layout/*`)

| Component | Import | Notes |
|-----------|--------|-------|
| `AppShell` | `AppShell` | Sidebar + optional topbar frame; owns sidebar `collapsed` state. `hideTopbar` prop. |
| `AppSidebar` | `AppSidebar` | Blue MindBridge nav rail; `collapsed` → icon rail with tooltips. |
| `AppTopbar` | `AppTopbar` | Hamburger + breadcrumb (prop-driven) + search + notifications + avatar. |

## Design tokens (semantic Tailwind classes)

Always prefer tokens over hardcoded colors — **never** `bg-[#...]` or raw hex.
Full list in [AGENTS.md](../../../AGENTS.md) and defined in
`design-system/styles/tokens.css`.

- **Core:** `bg-background`, `text-foreground`, `bg-card`, `bg-primary`, `bg-secondary`, `bg-muted`, `bg-accent`, `bg-destructive`, `bg-success`, `bg-warning`, `border-border`, `ring-ring`.
- **Sidebar:** `bg-sidebar`, `text-sidebar-foreground`, `text-sidebar-muted`, `bg-sidebar-accent`.
- **Risk:** `text-risk-high|medium|low`, cell fills `bg-risk-*-cell`, heat scale `bg-relative-*`.
- **Status:** `bg-status-open|resolved|verified|normal|manual`.
- **AI accent:** `bg-ai-bg`, `border-ai-border`, `text-ai-text`.
- **Charts:** `text-chart-1` … `text-chart-12` (Recharts series).

Dark mode: add the `.dark` class to `<html>`. Whitelabel themes: add a
`theme-*` class to `<html>` (see AGENTS.md).

## Figma component → code mapping

| Figma node name | Code component |
|-----------------|----------------|
| Button (Primary/Secondary/Neutral/Destructive/Text) | `Button` (`variant`) |
| Badge / Pill / Status | `Badge` (`variant`) |
| Text Input / Search | `Input` / `SearchInput` |
| Select / Dropdown | `Select` + parts |
| Modal / Dialog | `Dialog` + parts |
| Card | `Card` + parts |
| Tabs | `Tabs` + parts |
| Toggle / Switch | `Switch` |
| Checkbox | `Checkbox` |
| Avatar | `Avatar` |
| Breadcrumb | `Breadcrumb` + parts |
| Alert / Message | `Alert` + parts |
| Tooltip | `Tooltip` + parts |
| Spinner / Skeleton | `Spinner` / `Skeleton` |
| Table / Data grid | `Table` / `DataGrid` |
| Stepper | `Stepper` |

When `get_design_context` returns a node name not in this table, read
`reference.md`, check the component source, or fall back to a layout `div` with
semantic token classes.

**Dev/design annotations** in the `get_design_context` response can name the
intended component, state, or behavior directly. When present, let them drive
component choice — they override guesses from node names or the screenshot.

## Additional resources

- Where to find per-component prop APIs: [reference.md](reference.md)
- Design-system source (this repo, editable): `design-system/components/ui/*`, `design-system/components/layout/*`
- Barrel / export list: `design-system/index.ts`
- Tokens: `design-system/styles/tokens.css`
- Reusable composed sections: `blocks/` (browse via `/start-blocks`)
