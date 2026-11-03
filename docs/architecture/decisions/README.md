# Architecture Decision Records

Architecture Decision Records (ADRs) capture significant technical decisions and the reasoning behind them.

## When to write an ADR

Write an ADR when a decision materially affects system boundaries, public specifications, compatibility, security, data formats, build semantics, or long-term maintenance.

Routine implementation choices do not need an ADR.

## Lifecycle

1. Identify the problem and relevant constraints.
2. Discuss alternatives, preferably through an RFC when the decision is substantial or cross-cutting.
3. Write an ADR with context, decision, alternatives, and consequences.
4. Mark it **Proposed** while under review.
5. Mark it **Accepted**, **Rejected**, or **Superseded** after a decision.
6. Do not rewrite history when a decision changes; create a new ADR that supersedes the previous one.

## Naming

Use sequential identifiers and short kebab-case titles:

`ADR-0001-rust-workspace-structure.md`

## Template

Start from [template.md](template.md).
