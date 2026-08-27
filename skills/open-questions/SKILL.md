---
name: open-questions
description: Reads a PRD, spec, or design doc, finds every open-ended question and unresolved decision, researches a recommended answer for each, and presents them as decision-ready multiple-choice cards for the user to select from — then records the answers back into the doc. Use when the user runs /open-questions, shares a PRD/spec/plan and asks to address, resolve, or answer its open questions, or to turn "open questions / decisions to resolve" into concrete choices.
---

# Open Questions

Take a PRD (or spec, design doc, plan) and drive its open questions and undecided points to resolution: find every open-ended question or unresolved decision, research the best educated answer for each, present decision-ready multiple-choice cards using the `AskQuestion` tool, then record the user's decisions back into the source document.

This is scoped to what a document leaves **undecided** — explicit open-questions sections, inline "TBD / Open / unvalidated / needs X" markers, and choices that were discussed but never settled. (To surface *hidden* assumptions the doc never raised, use `examine-assumptions` instead.)

## Workflow

Copy this checklist and track progress:

```
- [ ] Step 1: Locate the source document
- [ ] Step 2: Extract every open question and undecided point
- [ ] Step 3: Research a recommended answer for each
- [ ] Step 4: Present decision cards with AskQuestion
- [ ] Step 5: Record the decisions back into the document
- [ ] Step 6: Repeat if answers open new questions
```

### Step 1: Locate the source document

If the user gave a path, read the whole file. If not, ask which document to work from. Read any docs it references (source meetings, related specs) when needed to understand a question's context.

### Step 2: Extract every open question and undecided point

Scan the whole document. Collect items in **both** of these buckets:

**Explicitly flagged as open:**
- Dedicated sections such as "Open questions", "Decisions to resolve", "TBD", "Risks", "Follow-ups"
- Inline markers: `Open`, `TBD`, `unresolved`, `unvalidated`, `unverified`, `needs decision`, `open for debate`, `deprioritized`, `deferred`, `blue sky`, `no final decision was made`
- Parentheticals assigning a dependency/owner: `(Needs Engineering)`, `(Needs Data/Platform)`, `(needs a design spike)`, `(revisit after ...)`
- Status tables where a row/column reads `Open`, `Open — needs X`, or `Confirmed for demo / Open long-term`

**Implicitly undecided:**
- Sentences phrased as questions ("should we…?", "which…?", "when should this be built?")
- Multiple options discussed with no choice made (e.g. "A vs B vs C were considered")
- Requirements that name a capability but leave the approach/mechanism unspecified
- Non-goals or "deferred" items that still hide a live decision (what triggers building it? does an existing pattern cover it?)

Preserve the document's own identifiers (e.g. `R6.2`, "Open Question #2") so every card is traceable back to its source. List each item plainly with a one-line note on where it came from before moving on.

### Step 3: Research a recommended answer for each

For each open item, form a confident **recommended default** to put in the card:
- Inspect the codebase first when the decision concerns existing conventions, components, data model, or scope (this repo: check `wireframes/<project>/src`, the `design-system/` library + its [catalog](../design-system-components/SKILL.md), the `blocks/`, and existing patterns before recommending anything new).
- Research online only when a confident answer isn't already available; prefer authoritative, current sources. Don't pad with needless searches.
- Ground recommendations in what already exists over inventing something new.

### Step 4: Present decision cards with AskQuestion

Turn each open item into one `AskQuestion` card. Do **not** list options as plain text — use the tool so the user can select directly. Batch related questions into a single `AskQuestion` call.

Each card must:
- **Explain the question in its `prompt`**: what the document leaves open (cite its ID/section), why it matters, the tradeoffs, and what your research/codebase inspection found — ending with your recommended default.
- Provide **3–4 concrete options**.
- Put the **recommended option first** and append `(Recommended)` to its label (the `AskQuestion` tool always adds an "Other" escape, so you don't need to add one manually; for genuinely open-ended items, still keep the option set tight).
- Use `allow_multiple: true` only when several answers can legitimately co-exist.

Keep one card per distinct decision — never merge unrelated questions into a single card.

### Step 5: Record the decisions back into the document

After the user answers, update the source document so it reflects the resolved decisions:
- Replace each open item with the chosen decision (keep the original ID).
- Update status tables: flip `Open` → `Confirmed`, note the chosen option.
- In the "Open questions" section, mark resolved items as decided (with the choice) and leave genuinely deferred ones with their new rationale.
- Preserve an audit trail — don't silently delete the history of what was open; show what was decided.

Confirm with the user before making large edits if the document is shared or authoritative.

### Step 6: Repeat if answers open new questions

Answers often expose follow-on decisions. Re-scan (Steps 2–4) until no undecided points remain that the user wants resolved.

## Card format

Mirror this shape when writing the `AskQuestion` prompt and options:

```
Q: Where should the agent chat live (final placement)?
Context: PRD R6.2 / Open Question #1 leaves placement open — side panel (as mocked),
floating button (like the existing Activity/Comments toggle in InsightActionPanels.tsx),
or a global top-bar entry in AppNavbar.tsx. The demo (R6.1) already commits to a side
panel next to Insight Detail, and the codebase has no top-bar chat entry today.
Building the trigger so it can be relocated (R6.2) keeps all three viable.
Recommended: keep the demo side-panel but decouple the trigger.
Options:
  A) Side panel next to Insight Detail, trigger decoupled for later relocation (Recommended)
  B) Floating button reusing the Activity/Comments pill pattern
  C) Global top-bar entry in the navbar
  D) Other / let me specify
```

As an `AskQuestion` call, the "Context" text goes in `prompt`, and A–D become `options` (recommended first, `(Recommended)` in its label; the tool adds "Other").

## Notes

- Cover the whole document, not just its "Open questions" section — inline `Open`/`TBD`/`unvalidated` markers and undecided tradeoffs count too.
- Don't invent decisions the document never raised; that's `examine-assumptions`' job.
- Always give a researched recommendation, not just a bare list — the user should be able to accept the default at a glance.
- Keep questions decision-ready: concrete options, clear tradeoffs, one decision per card.
- Some items are explicitly blocked on another team (Data/Platform, Engineering). For those, still present a card, but frame the options around next-step decisions (e.g. "spike now", "defer to team X", "descope") rather than pretending the blocker is resolvable here.
