# Component Reference

Unlike design-kit (which documents a prebuilt package), this kit **owns** its
design system as source. So the source **is** the reference — read the
component file directly for its exact props, variants, and defaults.

## Where to look

- **A specific component's props/variants:** open its source in
  `design-system/components/ui/<name>.tsx` (or `components/layout/<name>.tsx`).
  Variants live in the `cva(...)` call near the top; props are the exported
  `interface`/`type` (e.g. `ButtonProps`).
- **Everything the barrel exports:** `design-system/index.ts`.
- **Tokens / semantic classes:** `design-system/styles/tokens.css` and the
  token list in [AGENTS.md](../../../AGENTS.md).
- **Composed sections (blocks):** `blocks/*.tsx` + `blocks/index.json`.

## Common variants (quick recall)

- **Button** — `variant`: `default` (primary blue) · `secondary` (blue outline)
  · `neutral` (grey surface) · `destructive` · `outline` · `ghost` · `link`.
  `size`: `default` (34px) · `sm` · `lg` · `xs` · `icon`.
- **Badge** — roles `default`/`secondary`/`destructive`/`success`/`warning`/`outline`,
  plus MB vocab `valid`/`error`/`info`/`new`/`resolved`/`manual`/`normal`/`sparkle`.
- **Alert** — `variant`: `info`/`success`/`warning`/`error`.
- **Progress** — `tone`: `default`/`success`/`warning`/`destructive`.
- **Tabs** — list `variant`: `underline`/`pill`/`nav`.

When in doubt, grep the file — the CVA config is the source of truth, and it can
change as the design system evolves.
