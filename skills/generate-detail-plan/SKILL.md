---
name: generate-detail-plan
description: Generates a detailed implementation plan with technical design and code snippets, structured as a checklist that links to each task section via anchor links. Use when the user runs /generate-detail-plan or asks for a detailed implementation/technical plan for a feature or project.
---

# /generate-detail-plan — Detailed Implementation Plan

Generate a detailed implementation plan with technical design and code snippets when helpful. The plan must start with a checklist that links to each task section (anchor links). Include instructions for developers to check off items as work progresses.

## Steps

1. Understand the scope — read the feature request/brief and any referenced code/files to ground the plan in the actual codebase.
2. Break the work into **phases**, and each phase into numbered **tasks** (e.g. `0.1`, `0.2`, `1.1`, ...).
3. Write a **Progress Tracker** checklist section first, with one `- [ ]` item per task, each linking via a markdown anchor to that task's detail section below.
4. Write one detail section per task, including: what to do, files to check/update, implementation steps, and a validation checklist.
5. Save the plan as a markdown file (ask the user for a filename/location if not specified, otherwise default to a sensibly named file in the project root or a `plans/` directory if one exists).

## Few-shot example (structure and tone)

Use this as a template for headings, checklist format, and section depth:

```md
# <Project/Feature> – Detailed Implementation Plan

<One-paragraph scope summary>

**Instructions for developers:**
- Check off each item `[ ]` → `[x]` as you complete it, also add emoji checkmark.
- Each checklist item links to its detailed task section below (use anchor links).

---

## Progress Tracker (Checklist)

### Phase 0: <Phase Title>
- [ ] [0.1](#01-<anchor-title>) <Task title>
- [ ] [0.2](#02-<anchor-title>) <Task title>

### Phase 1: <Phase Title>
- [ ] [1.1](#11-<anchor-title>) <Task title>

### Phase N: <Phase Title>
- [ ] [N.1](#n1-<anchor-title>) <Task title>

---

## Phase 0: <Phase Title>

### 0.1 <Task title>

**Task:** <What to do>

**Files to check/update:**
- `<path/to/file>`

**Implementation:**
- <Step 1>
- <Step 2>

**Validation:**
- [ ] <Check>

---

## Phase N: <Phase Title>

### N.1 <Task title>

**Task:** <What to do>

**Validation:**
- [ ] <Check>
```

## Notes

- Include code snippets in task detail sections whenever they clarify the intended implementation (e.g. a function signature, a component prop shape, a config change) — keep them short and focused, not full file dumps.
- Anchor links must match GitHub/markdown's auto-generated heading slugs (lowercase, spaces → `-`, punctuation stripped).
- Once the plan is generated, follow-up work on it typically uses `/next-phase` to execute one phase at a time.
