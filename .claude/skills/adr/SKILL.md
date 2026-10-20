---
name: adr
description: Create, compare, review, and record Architecture Decision Records (ADRs). Use when the user invokes /adr or asks to document a technical decision.
argument-hint: "make <topic> | options <ADR-ID> | review <ADR-ID> | decide <ADR-ID> | list"
---

# ADR workflow

You manage ADR documents in `docs/adr/`. Follow the user's requested subcommand from `$ARGUMENTS`.

## Global rules

- Begin with the problem and desired outcome; do not assume the user's proposed solution is correct.
- Explore the repository and relevant docs before making claims about existing architecture.
- Clearly label information as:
  - **Fact**: confirmed by repository, requirements, or supplied evidence.
  - **Assumption**: plausible but not confirmed.
  - **Hypothesis**: a prediction that needs validation.
  - **Measured evidence**: backed by an actual test, benchmark, query plan, or operational observation.
- Never invent traffic, data volume, latency, cost, or benchmark figures.
- Consider the status quo as an option when it is viable.
- Compare trade-offs, operational cost, migration cost, security, data integrity, performance, and future change cost where relevant.
- Do not make a final decision for the user. `/adr decide` records a decision only after explicitly confirming the user's choice.
- Do not run destructive commands, deploy, or commit changes unless the user separately requests and confirms the action.
- Keep ADRs concise, specific, and understandable without the chat transcript.
- Use the template in `references/adr-template.md` and the checklist in `references/decision-checklist.md`.
- Preserve history: do not silently rewrite an accepted ADR into a different decision. Create a new ADR and mark the previous one as superseded when appropriate.

## Mode and file-writing behavior

For analysis-heavy work, recommend that the user enter Claude Code Plan Mode using `/plan` before invoking this skill. A Skill does not itself guarantee a switch of the interactive session's permission mode. If not in Plan Mode, first analyze and present the proposed plan; ask before writing files. Do not claim that Plan Mode is active unless the user has confirmed it or the interface indicates it.

## Subcommands

### `make <topic>`

1. Read `docs/adr/README.md` and the ADR template.
2. Inspect relevant project files and existing ADRs. Do not scan unrelated files indiscriminately.
3. Restate the problem, desired outcome, stakeholders, constraints, and known non-goals.
4. Separate confirmed facts from assumptions and unanswered questions.
5. If a critical detail is missing, ask one focused question at a time. Otherwise draft a proposed ADR.
6. Assign the next available sequential ID (`ADR-001`, `ADR-002`, ...). Check existing files to avoid collisions.
7. Draft the ADR with status `Proposed`. Do not choose a final option merely because the user mentioned one.
8. Show the planned file path and a concise summary. Ask before writing if the current mode or user request does not clearly authorize writing.

### `options <ADR-ID>`

1. Read the target ADR and relevant project context.
2. Identify at least two viable options when alternatives genuinely exist. Include the status quo when relevant.
3. For each option, document: intent, advantages, costs, risks, implementation/migration effort, and conditions where it fits.
4. Compare the options against the ADR's decision drivers. Explain when a factor is a hard constraint versus a preference.
5. Identify missing evidence and propose the cheapest useful validation (for example, query-plan inspection, a small benchmark, or a requirements check).
6. Avoid false precision and arbitrary weighted scores unless the user requests them and agrees on weights.
7. Update the ADR's options section only after presenting the analysis; do not mark any option Accepted.

### `review <ADR-ID>`

Review the ADR as a critical peer reviewer. Check:
- Is the problem framed independently from the proposed solution?
- Are requirements, facts, assumptions, and hypotheses distinguished?
- Are meaningful alternatives considered, including the status quo?
- Are trade-offs and rejected alternatives explained?
- Are data integrity, security, operations, performance, migration, and maintainability relevant and covered?
- Are claims supported by repository evidence, documentation, or measurements?
- Are consequences, validation steps, and revisit conditions actionable?
- Is the decision reversible, and what is the cost of reversal?
Return findings by severity: Blocker, Important, Minor. Suggest edits but do not silently change the decision.

### `decide <ADR-ID>`

1. Read the ADR and summarize the options, key trade-offs, unresolved risks, and recommendation (if one exists).
2. Ask the user to explicitly select an option and confirm any conditions.
3. Only after confirmation, update status to `Accepted`, record the chosen option and rationale, document consequences and validation, and identify any superseded ADRs.
4. If the user has not chosen, leave status as `Proposed`.
5. Do not commit changes automatically.

### `list`

List ADR files with ID, title, status, and a one-line summary. If a status cannot be established from the document, label it `Unknown` rather than guessing.

## Output expectations

At the end of each operation, report:
- files read or changed,
- what is confirmed versus assumed,
- open questions or risks,
- the next useful step.

Keep the response concise. Do not repeat the full ADR unless requested.
