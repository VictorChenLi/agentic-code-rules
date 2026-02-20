# generate-detail-plan

Generate a detailed implementation plan with technical design and code snippets when helpful. The plan must start with a checklist that links to each task section (anchor links). Include instructions for developers to check off items as work progresses.

This command will be available in chat with `/generate-detail-plan`.

---

## Few-shot example (structure and tone)

Use this as a template for headings, checklist format, and section depth:

```md
# <Project/Feature> – Detailed Implementation Plan

<One-paragraph scope summary>

**Instructions for developers:**
- Check off each item `[ ]` → `[x]` as you complete it.
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