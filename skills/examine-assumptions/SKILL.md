---
name: examine-assumptions
description: Surfaces and stress-tests hidden assumptions in a plan, design doc, or proposal, then drives them to resolution through researched, multiple-choice clarifying questions and updates the plan. Use when the user shares a plan, spec, PRD, or design and asks to examine assumptions, find unverified assumptions, pressure-test the plan, or asks clarifying questions before implementation.
---

# Examine Assumptions

Take a plan (or design doc, spec, PRD, proposal) the user shared and iteratively surface every hidden or unverified assumption, research the best educated answer for each, turn them into decision-ready multiple-choice questions, and finally update the plan based on the user's answers.

## Workflow

Copy this checklist and track progress:

```
- [ ] Step 1: Extract and examine assumptions in the plan
- [ ] Step 2: Research the best educated answer for each assumption
- [ ] Step 3: Generate multiple-choice clarifying questions
- [ ] Step 4: Repeat 1-3 until no unverified assumptions remain
- [ ] Step 5: Update the plan based on the answers
```

### Step 1: Extract and examine assumptions

Review the plan the user shared. Extract and examine the assumptions that **you or the document** have made. Look for:

- Implicit technical choices (libraries, versions, protocols, data formats, infra)
- Unstated requirements, constraints, scope boundaries, and success criteria
- Assumptions about scale, performance, security, cost, or compliance
- Dependencies on other systems, teams, or external services
- "Obvious" defaults that were never explicitly decided

List each assumption plainly and note whether it was made by the document or inferred by you.

### Step 2: Research the best educated answer

For each assumption, research online **if necessary** to find the best educated answer. Use that finding as context for the question you will generate. Prefer authoritative, current sources (official docs, primary references). Inspect the codebase when the assumption concerns existing project conventions.

### Step 3: Generate multiple-choice clarifying questions

Generate a list of clarifying questions from Step 2. Each question must:

- Provide **3-4 options** for the user to select from
- Include the context you researched to inform the decision (cite what you found and your recommended default)

Use the `AskQuestion` tool to present these so the user can select directly, rather than listing options as plain text.

### Step 4: Repeat until exhausted

Repeat Steps 1-3 until there are no more hidden, unverified assumptions left in the plan. Each pass may reveal new assumptions exposed by the previous answers.

### Step 5: Update the plan

Based on all the answers, update the plan the user shared so it reflects the resolved decisions and removes the now-settled assumptions.

## Question format

When presenting questions, give each one researched context plus a recommended default:

```
Q: Which session storage approach should the auth flow use?
Context: The plan assumes JWTs but never states storage. Industry guidance favors
httpOnly cookies over localStorage for XSS resistance. Recommended default: B.
Options:
  A) localStorage (simplest, but XSS-exposed)
  B) httpOnly secure cookie (recommended)
  C) In-memory + silent refresh
  D) Other / let me specify
```

## Notes

- Surface assumptions you yourself introduced while reading, not just the document's.
- Only research when a confident answer isn't already available; don't pad with needless searches.
- Always include an "Other / let me specify" style escape option when the choice is open-ended.
- Keep iterating; do not stop at the first batch of questions if answers reveal new gaps.
