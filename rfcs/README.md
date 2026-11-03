# Requests for Comments (RFCs)

The RFC process is used to develop and review substantial changes to CXXForge before implementation or adoption.

## When an RFC is expected

Use an RFC for changes to:

- Public package, manifest, lockfile, or registry specifications.
- Dependency resolution semantics.
- Build graph and execution semantics.
- Toolchain, target, or ABI compatibility policy.
- Security and trust boundaries.
- Major subsystem boundaries or compatibility guarantees.

Small bug fixes, internal refactors, and routine documentation improvements generally do not need an RFC.

## Process

1. Open an issue describing the problem and intended outcome.
2. Create a proposal from [template.md](template.md).
3. Submit it as a pull request under `rfcs/` with a sequential identifier.
4. Discuss alternatives, compatibility, security, migration, and implementation impact.
5. The project lead or delegated maintainers record the outcome: **Draft**, **In Review**, **Accepted**, **Rejected**, or **Withdrawn**.
6. If accepted, create or update the relevant specifications and ADRs.
7. Link implementation work to the accepted RFC.

Acceptance of an RFC approves the direction; it does not mean the implementation is complete.

## Naming

Use `RFC-NNNN-short-title.md`, for example `RFC-0001-package-identity.md`.

## Review expectations

A good RFC defines the problem, goals, non-goals, proposed design, alternatives, compatibility implications, security considerations, testing strategy, and unresolved questions.

The process is intentionally lightweight while the project is small. Governance may formalize review periods and decision rules as the maintainer community grows.
