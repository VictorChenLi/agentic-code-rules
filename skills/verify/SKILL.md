---
name: verify
description: Self-verification loop that compares a built wireframe screen against its source spec (Figma screenshot, uploaded image, or text brief). Run after every screen is built, before telling the designer the work is done. Catches label mismatches, wrong component types, incorrect mock data, and missing/extra UI elements.
---

# /verify — Spec-vs-Code Verification Loop

Run this skill **after every screen is built** and before declaring done.

---

## Step 0 — Ask before verifying (MANDATORY)

Verification is **opt-in**. Before doing any verification work, ask the designer
whether they want it — do not start automatically.

On **each build iteration**, ask two things:

1. **Do you want to verify this screen at all?** If no, skip and continue.
2. **If yes, full or quick?**
   - **Full** — run the complete Step 1–5 checklist below.
   - **Quick** — run only design-system fidelity + design tokens (Step 2 items
     11–12) and the TypeScript check (Step 5). Skip the pixel-level diff.

Default to **quick** if unspecified.

### Cloud agents

When running as a **cloud agent**, do **not** capture screen recordings or
screenshots. Verify code-and-reference only: compare the built code against the
source spec (Figma screenshot from `get_screenshot`, the uploaded image, or the
brief) plus the TypeScript check.

### Local agents — UI screenshots

Use the **Cursor built-in browser** for visual checks. Start the dev server on
port **5173** bound to `127.0.0.1`, confirm readiness with `curl`, then navigate
to `http://localhost:5173/` (see [AGENTS.md](../../../AGENTS.md) / the built-in
browser rule). Never fall back to `screencapture`/AppleScript.

---

## Step 1 — Obtain the reference

- **Figma URL:** call `get_screenshot` with the same `fileKey`/`nodeId` used at
  intake. Re-read any **dev/design annotations** (`get_design_context`).
- **Uploaded screenshot:** re-read the image file; don't rely on memory.
- **Text brief:** skip to Step 3.

---

## Step 2 — Visual diff checklist

Compare the reference against your code on every axis. Mark each ✅ or ❌.

| # | Axis | What to check |
|---|---|---|
| 1 | Navigation / breadcrumb | Exact labels, separators, icons |
| 2 | View-mode controls | Tabs vs pills vs dropdown; exact label text |
| 3 | Filter bar | Exact filter labels, count, active chips, "Clear" wording |
| 4 | Section sub-header | Tab labels/order, stepper format |
| 5 | Column headers | Exact names (incl. units), order, sort indicator |
| 6 | Mock data — rows | Values match the spec — never invent alternatives |
| 7 | Status badges | Label text, variant, pill vs dot |
| 8 | Conditional icons | Render only where the spec shows them |
| 9 | Row count | Matches the spec |
| 10 | Dark / light mode | If spec is dark, add `class="dark"` to `<html>` |
| 11 | **Design-system fidelity** | Every interactive/visual element is a `@platform/design-system` component — **not** a hand-rolled `div`/`button`. Plain `div`/`span`/`section` only for layout. If a primitive is missing, it was added to `design-system/components/ui/` (not hand-rolled inline). For a full element-by-element pass, run [design-system-validation](../design-system-validation/SKILL.md). See [design-system-components](../design-system-components/SKILL.md). |
| 12 | **Design tokens** | Colors/spacing/elevation use token classes (`bg-card`, `text-foreground`, `border-border`, `shadow-elevation`, …) — no hardcoded hex or `bg-[#...]`. |
| 13 | **Dev/design annotations** | Every annotation is reflected — states, behavior, copy, component choices. |

---

## Step 3 — Logic review (text brief only)

Confirm every stated feature is implemented: each named screen exists, each
interaction has a handler, no stated data field is missing.

---

## Step 4 — Fix all discrepancies

For every ❌: identify the line(s), apply the fix, re-check that item. Fix them
all autonomously — don't hand the designer a list.

---

## Step 5 — Final TypeScript check

```bash
cd wireframes/<project-name>
npm run typecheck
```

This checks the wireframe **and** the shared design-system source it imports.
Fix any errors in your files before proceeding.

---

## Step 6 — Done signal

Only after the checklist is ✅ and TypeScript is clean:
- Confirm the dev server is running (`npm run dev -- --port 5173 --host 127.0.0.1`)
- Tell the designer the localhost URL
- Summarise what the screen shows
