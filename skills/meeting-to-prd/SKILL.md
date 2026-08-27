---
name: meeting-to-prd
description: Turn a meeting transcript or notes plus the existing codebase into a structured PRD that captures new requirements and teammate feedback. Use when the user provides a meeting recording transcript, call notes, or review feedback and asks to create, draft, or update a PRD, spec, or requirements doc from it.
---

# Meeting → PRD

Convert a meeting transcript (and any supporting notes) into a requirements PRD that
(1) faithfully captures what each teammate said, and (2) is grounded in the **actual current
codebase** — not assumptions. The output mirrors the structure of
`context/scenario-ux-improve-0624/scenario-ux-prd-0624.md` (generated from
`context/scenario-ux-improve-0624/Forecast V2 Progress Check-In.txt`).

## Core principles

1. **Feedback ≠ requirements.** For each topic, first write what was said (attributed to people),
   then translate it into numbered, testable requirements (R1.1, R1.2, …). Never invent requirements
   no one asked for; never drop feedback because it's inconvenient.
2. **Verify against code.** Before writing the "what the system does today" context, read the
   relevant source files and cite them by name (e.g. `ScenarioConfigPanel.tsx`, `applyDriverChange`).
   If the transcript claims a behavior, confirm it in code or flag it as unverified.
3. **Attribute.** Tie feedback to the person who raised it (e.g. "relabel to current year (Fiona)").
   This preserves intent and lets readers follow up.
4. **Capture open decisions.** Disagreements, deferrals, and "we'll follow up offline" become
   explicit **Open questions** with an owner — don't resolve them silently.
5. **Plain language.** Frame requirements in the user's/domain terms, not internal mechanics.
6. **Scope discipline.** Record what's explicitly out (non-goals) and deprioritized, with the reason.

## Workflow

Copy this checklist and track progress:

```
- [ ] Step 1: Read all source material (transcript + notes the user points to)
- [ ] Step 2: Extract topics, feedback, and decisions (attributed)
- [ ] Step 3: Verify current behavior against the codebase
- [ ] Step 4: Draft requirements per topic (numbered R#.#)
- [ ] Step 5: Assemble the PRD from template.md
- [ ] Step 6: Self-review against the quality checklist
```

**Step 1 — Read sources.** Read the transcript(s)/notes in full. Note the meeting name, date, and
participants. If the user references more than one source (e.g. a group recording + working notes),
read them all and list each in the PRD header + appendix.

**Step 2 — Extract.** Group the discussion into distinct topics (one topic ≈ one `## 4.x` section).
For each, jot: the feedback (who said what), any agreed direction, and any unresolved decision.
Distinguish a confirmed decision ("we'll relabel X→Y") from an open one ("we'll follow up offline").

**Step 3 — Verify against code.** For every claim about current behavior, locate the implementing
code and confirm it. Use Grep/SemanticSearch to find the files. Cite specific files/functions in the
"Context — what the current prototype does (verified against code)" subsection. Mark anything you
could not confirm as *(unverified)*.

**Step 4 — Draft requirements.** Translate feedback into numbered requirements grouped by topic
(R1.x, R2.x, …). Each requirement is a single, testable statement. Where a requirement matches
existing code, note it (e.g. *(Matches current `applyDriverChange`.)*). Where it needs another team,
name them (e.g. "Engage Data Science to define the formula").

**Step 5 — Assemble.** Build the document using [template.md](template.md). Fill every section;
delete a section only if it is genuinely empty (and prefer writing "None" over deleting).

**Step 6 — Self-review.** Run the quality checklist below before declaring done.

## Output location & naming

- Default to the same folder as the source transcript, named `<topic>-prd-<MMDD>.md`
  (e.g. a transcript in `context/scenario-ux-improve-0624/` → `scenario-ux-prd-0624.md`).
- If the user specifies a path or name, follow it. If unclear, ask once.

## Quality checklist

- [ ] Header lists every source meeting/file, date, participants, author, status, related docs
- [ ] "Current behavior" subsection cites real files/functions (verified), not guesses
- [ ] Every topic has both a **Feedback** block (attributed) and numbered **Requirements**
- [ ] Goals and non-goals are explicit; deprioritized items state the reason
- [ ] A functional-summary table maps each requirement group to a decision/status
- [ ] Open questions list owners
- [ ] No requirement appears that no one in the meeting asked for
- [ ] Plain-language framing; consistent terminology throughout

## Template

The full PRD skeleton (sections, tables, and the Feedback→Requirements pattern) is in
[template.md](template.md). Read it before assembling Step 5.
