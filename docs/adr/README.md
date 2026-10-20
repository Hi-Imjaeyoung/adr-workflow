# Architecture Decision Records

This directory stores durable records of important technical decisions.

## Naming

Use `ADR-NNN-short-kebab-case-title.md`, for example:

- `ADR-001-content-storage-model.md`
- `ADR-002-authentication-session-strategy.md`

Use sequential IDs. Never reuse an ID after an ADR is rejected or superseded.

## Status

- `Proposed`: under discussion; no final decision.
- `Accepted`: decision owner approved the choice.
- `Rejected`: the proposal was considered and rejected.
- `Superseded`: a later ADR replaces this decision.
- `Deprecated`: no longer applicable.

## Guidelines

- Write for a future teammate who was not part of the original discussion.
- Record why a choice was made, not just what was implemented.
- Distinguish confirmed facts from assumptions and measurements.
- Keep the record concise and link to issues/PRs for implementation detail.
- When an accepted decision changes materially, create a new ADR and link both records.
- Do not store credentials, secrets, personal data, or sensitive production details in ADRs.

## Template

The reusable template is maintained at `.claude/skills/adr/references/adr-template.md`.
