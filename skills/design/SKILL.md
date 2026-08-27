---
name: design
description: Starting point for creating live wireframes in the platform-design-kit. Accepts a text brief, uploaded screenshots, or a Figma URL/selection (via Figma MCP). Orchestrates use-blocks, scaffold-wireframe, design-system-components, verify, save-block, and deploy. Use when a designer runs /design, mentions wireframe, prototype, or screen, or provides a Figma link to implement as a live React app.
---

# /design — Wireframe Orchestrator

Entry point for all wireframing sessions. Accept whatever the designer provides
and drive the full flow. Screens are built with the **local**
`@platform/design-system` (this kit builds its own components — see
[design-system-components](../design-system-components/SKILL.md)).

## Intake (step 1)

Accept any combination of:

- **Text brief** — feature description, user flow, notes
- **Screenshots** — attach images directly; read them to extract layout intent
- **Figma URL or current selection** — call `get_design_context` to extract
  frame structure, component names, spacing, and tokens

If a Figma URL is given, call `get_design_context` immediately and map:
- Page/frame names → routes or views
- Component names → the closest `@platform/design-system` component (see the
  [catalog](../design-system-components/SKILL.md))
- Colors/spacing → design token classes (`bg-primary`, `bg-card`, `border-border`, …)
- **Dev/design annotations** → read them and treat them as authoritative intent

### Dev annotations (always check)

When a source has developer/design annotations, they capture the designer's
explicit intent — behavior, states, edge cases, copy, or "use component X"
notes. In Figma, `get_design_context` surfaces these as **Design annotations**;
in screenshots/briefs, treat callouts, sticky notes, and redlines the same way.
Honor annotations as high-priority intent; if one conflicts with the raw
layout, follow the annotation. If an annotation asks for something outside the
design system or this kit's scope, stop and tell the designer.

## Browse blocks first (step 2)

Read and follow [`use-blocks`](../use-blocks/SKILL.md) — check `blocks/index.json`
for a reusable section that matches the design before building from scratch.

## Clarifying questions (step 3)

Ask at most **two** questions before starting:

1. **Project name** — the wireframe folder (`wireframes/<name>`).
2. **Starting point** — **clean slate** (empty `templates/wireframe`),
   **base project** (copy `wireframes/platform-clients-demo`), or add to an
   **existing wireframe** in `wireframes/`.

Skip questions you can infer from context. When in doubt for a MindBridge
platform flow, the base project is usually the faster start.

**What the base project already contains** — copying it inherits a working
prototype, so check whether the brief is really a new build:

| Surface | Where | What you get |
|---|---|---|
| General Ledger Analysis | `pages/risk-overview.tsx` | The analysis page and its tab strip (financial statements, trends, ratios, risk overview, risk segmentation, monetary flow, data table, annotations, reports) |
| Risk lens | `pages/risk-lens.tsx` | Import → simulated analysis → reconciliation list (flat + grouped, filters, batch decisions) → mapping detail with evidence tabs and a decision popover → export/handoff |
| Audit assertion risk | `pages/audit-assertion-risk.tsx` | Account × assertion heat table → assertion detail (control points, entries) → journal drill-down, cross-linked with Risk Lens |
| Admin | `pages/admin/` | Opened from the sidebar's `admin` row. RMM libraries and Libraries are built (including the RMM → account-group mapping flow); the other eight tabs are placeholders |

Everything runs on typed fixtures in `src/data/*` — no network, no persistence.
Delete the surfaces your brief does not need instead of leaving dead tabs.

## New project flow (step 4a)

Read and follow [`scaffold-wireframe`](../scaffold-wireframe/SKILL.md), passing
the chosen starting point. Then return here. When starting from the **base
project**, adapt/rename/extend the existing screens rather than deleting them.

## Build screens (step 4b — new or existing)

Read the [design-system-components](../design-system-components/SKILL.md) catalog,
then build iteratively:

1. Create one screen at a time as `src/screens/<ScreenName>.tsx` (or reuse the
   base project's `src/pages/*`).
2. Wire screens into `src/App.tsx` (simple in-memory routing with state is fine).
3. Use mock data inline or in `src/data/*` — no API calls, no backend.
4. Import UI from `@platform/design-system`; icons from `lucide-react`.
5. Use design token classes for all colors — never hardcode hex.
6. Toggle dark mode via the `.dark` class on `<html>`.

If a needed primitive genuinely doesn't exist, add it to
`design-system/components/ui/` (shadcn + token style) and export it from
`design-system/index.ts` — don't hand-roll a one-off or pull in a third-party kit.

## Constraints (always enforce)

- Design-system first — compose from `@platform/design-system`; only extend the
  library when a primitive is truly missing.
- Frontend only — no API routes, database, or auth logic.
- Mock data only — realistic but obviously fake.
- No tests, no new runtime dependencies without a clear reason.

## Verify (step 5 — ask first, after each screen)

After each screen is built, **ask the designer whether they want verification**
(and if so, full or quick) — do not verify automatically. Then read and follow
[`verify`](../verify/SKILL.md).

## Save blocks (step 6 — after verify passes or is skipped)

Scan the completed screen for self-contained, reusable sections. For each good
candidate, read and follow [`save-block`](../save-block/SKILL.md). If none are
found, say so explicitly — don't silently skip.

## Done signal

After verify passes/declines, blocks are saved (or skipped), and TypeScript is
clean, run `npm run dev -- --port 5173 --host 127.0.0.1` in the wireframe dir,
confirm it starts, and tell the designer the localhost URL and what to look for.

## Deploy

When the designer is ready to share, read and follow [`deploy`](../deploy/SKILL.md).
