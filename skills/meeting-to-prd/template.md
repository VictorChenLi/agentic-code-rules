# PRD Template (Meeting → PRD)

Fill every section. Keep the **Feedback → Requirements** pattern in section 4 — it is the heart of
the document. Replace bracketed placeholders. Use plain, domain language.

---

```markdown
# PRD: [Feature / Area] — [Theme] ([Month DD, YYYY])

**Source meetings:**
- "[Meeting name]" — [date] ([group review / working notes]). Transcript: `[path]`
- "[Second source, if any]" — [date]. Transcript: `[path]`

**Author:** [Name] ([one-line note, e.g. consolidating feedback before next iteration])
**Status:** [Draft / In review / Approved]
**Participants:** [comma-separated names from the session]
**Related docs:** `[path]`, `[path]`

---

## 1. Overview

### 1.1 Purpose
[1 short paragraph: why this doc exists and what it changes. State the goal of the work —
e.g. simplify / clarify / restructure / add X.]

### 1.2 Context — what the current system does (verified against code)
[Bullets describing today's behavior, each grounded in a real file/function. Mark anything
you could not confirm as *(unverified)*.]
- [Behavior] (`File.tsx`).
- [Behavior] (`service.ts`, `functionName`).

### 1.3 Themes from the [date] review
[Numbered one-line summaries of the major takeaways, in priority order.]
1. [Theme]
2. [Theme]

---

## 2. Problem statement
[Prose: the user/domain pain in their own terms, and the core confusions. End with the
guiding principle for the fix.]

---

## 3. Goals & non-goals

### 3.1 Goals
- [Outcome-oriented goal]
- [Outcome-oriented goal]

### 3.2 Non-goals
- [Explicitly out of scope] ([reason]).
- [Deprioritized] ([reason / deferred to later release]).

---

## 4. Detailed feedback → requirements

### 4.1 [Topic title]

**Feedback**
- [What was said, attributed] ([Name]).
- [What was said] ([Name]).

**Requirements**
- **R1.1** [Single testable requirement.]
- **R1.2** [Single testable requirement.] *(Matches current `code` / Needs [team].)*

### 4.2 [Next topic]

**Feedback**
- [...] ([Name]).

**Requirements**
- **R2.1** [...]
- **R2.2** [...]

[Repeat 4.x for each distinct topic. Number requirement groups R1, R2, R3, … to match sections.]

---

## 5. Functional summary (new/changed)

| ID | Area | Requirement | Decision / status |
|----|------|-------------|-------------------|
| R1 | [area] | [one-line summary] | [Confirmed / Open / Needs X] |
| R2 | [area] | [one-line summary] | [Confirmed / ...] |

---

## 6. UX requirements
[Cross-cutting UX principles distilled from the feedback — copy tone, disclosure, labeling, etc.]
- **[Principle]:** [what it means concretely].

---

## 7. Open questions / decisions to resolve
[Every unresolved decision, with an owner.]
1. **[Question] (R#.#):** [context]. — *[Owner].*
2. **[Question]:** [context]. — *[Owner].*

---

## 8. Process & next steps
- **Cadence:** [meeting rhythm / target date].
- **This iteration's build focus:** [the requirements being built now].
- **Follow-ups:** [who does what before next session].

---

## 9. Appendix: source meetings
- **[Meeting name]** ([date]) — [one-line description of what it covered].
- **[Second source]** ([date]) — [one-line description].
- **Client signal:** [external signal, if any] — [note].
```

---

## Notes on filling this in

- **Requirement IDs:** group number matches section number (section 4.3 → R3.x). The summary table
  rolls each group up to a single `R#` row.
- **Decision/status values:** prefer `Confirmed`, `Open`, or `Needs [team]` — keep it terse.
- **When code contradicts the transcript:** trust the code, and note the discrepancy in the relevant
  Feedback/Requirements block rather than silently picking one.
- **Deferred topics:** still record them (as a non-goal or a `4.x` "Deprioritized" section) with the
  reason — don't drop them.
