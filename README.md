# ADR Workflow for Claude Code

A lightweight, Git-friendly workflow for making and reviewing Architecture Decision Records (ADRs) with Claude Code.

> Status: starter template / early prototype. Review the workflow in your own repository before relying on it for consequential decisions.

## What it does

- `/adr make <topic>` — create an ADR draft and define the problem.
- `/adr options <ADR-ID>` — compare plausible alternatives and trade-offs.
- `/adr review <ADR-ID>` — challenge assumptions, evidence, and completeness.
- `/adr decide <ADR-ID>` — record the human-approved decision and consequences.
- `/adr list` — list ADRs and their status.

The workflow is designed to keep **facts, assumptions, hypotheses, and measured evidence distinct**. Claude can help analyze options, but a human owns the final decision.

## Install in a project

Copy the `.claude/` and `docs/` directories into your project root. Then start Claude Code in that repository and run:

```text
/adr make content-storage-model
/adr options ADR-001
/adr review ADR-001
/adr decide ADR-001
/adr list
```

Use your own topic wording; the ID is assigned based on the next available number.

## Plan Mode limitation

Claude Code Skills provide reusable instructions and can be invoked as slash commands, but a skill should not be assumed to switch the interactive session's permission mode by itself. For a genuinely read-only planning pass, enter Plan Mode with `/plan` (or the relevant keyboard shortcut in your version), then run `/adr make ...` or `/adr options ...`.

The skill instructs Claude to plan before editing and to ask before recording a final decision. Treat this as workflow guidance, not a security boundary. Verify behavior against the Claude Code version you use.

## Suggested repository layout

```text
.claude/
  skills/
    adr/
      SKILL.md
      references/
        adr-template.md
        decision-checklist.md
docs/
  adr/
    README.md
    000-template.md
```

## Status model

- `Proposed` — the question is open; options may still be explored.
- `Accepted` — a human approved the decision.
- `Rejected` — this option/decision was considered and rejected.
- `Superseded` — a later ADR replaces it.
- `Deprecated` — the decision is no longer applicable.

Avoid rewriting history silently. When a decision changes, create a new ADR and link the older record to it.

## Git workflow

1. Create/update an ADR on a feature branch.
2. Review the diff like code.
3. Ask a reviewer to challenge assumptions and trade-offs.
4. Commit the ADR with the related implementation when practical, or in a dedicated documentation commit.
5. If the decision changes, create a new ADR and mark the previous one as superseded.

Example commit message:

```text
docs(adr): record content storage decision
```

## Design principles

1. Start with the problem, not a preferred solution.
2. Compare at least two viable options when meaningful.
3. Include the status quo as an option when relevant.
4. Distinguish requirements from assumptions.
5. Do not invent benchmarks or expected scale.
6. State consequences and revisit conditions.
7. Human approval is required before setting a decision to `Accepted`.
8. Prefer a small, useful ADR over a large speculative document.

## License

MIT. See `LICENSE`.
