# Architecture Decision Records

Architecture Decision Records (ADRs) document significant technical decisions that shape CXXForge.

## When to write an ADR

Create an ADR when a decision:

- Establishes or changes a major architectural boundary.
- Selects a foundational technology or protocol.
- Constrains future compatibility, extensibility, security, or deployment.
- Resolves a significant trade-off between competing architectural approaches.

Routine implementation details do not need an ADR.

## Naming

Use a monotonically increasing four-digit number and a short, descriptive slug:

`0001-modular-monolith.md`

Do not reuse an ADR number, including for rejected or withdrawn decisions.

## Required structure

Use the [ADR template](template.md). Include context, decision, alternatives considered, consequences, status, date, and related documents.

## Status

- **Proposed** — under consideration.
- **Accepted** — approved by the founder.
- **Rejected** — considered and not selected.
- **Superseded** — replaced by a later ADR.
- **Withdrawn** — proposal abandoned before acceptance.

An accepted ADR is immutable in its decision history. If the decision changes, create a new ADR and mark the earlier one superseded.

## Approval and publication

The founder is the final approval authority. ADR changes are published through pull requests under the [documentation governance policy](../../development/documentation-governance.md).

## Records

Add accepted, rejected, withdrawn, and superseded ADRs to this directory. Keep this index updated with links and current status.
