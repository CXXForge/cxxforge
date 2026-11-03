# Documentation Governance

- Status: Accepted
- Approval authority: Founder
- Publication workflow: Pull request
- Effective date: 2026-11-03

## 1. Purpose

This policy defines how CXXForge documentation is drafted, reviewed, approved, published, and maintained. It prevents conflicting sources of truth and makes architectural changes traceable.

## 2. Canonical source of truth

The CXXForge GitHub repository is the canonical source of truth for project documentation.

Chat conversations, notes, and working drafts may be used to explore and develop proposals, but they are not authoritative project specifications. A proposal becomes authoritative only after explicit founder approval and publication through the repository workflow.

Documentation is maintained in Markdown unless a specific technical format provides a clear benefit.

## 3. Document categories

### 3.1 Architecture specifications

Specifications describe the intended architecture, system behavior, interfaces, constraints, and technical requirements. They are maintained as stable files whose history is tracked by Git.

### 3.2 Architecture Decision Records (ADRs)

ADRs record significant architectural decisions, including context, the decision, alternatives, and consequences. Once accepted, an ADR is not rewritten to conceal a change of direction. A later ADR records the new decision and identifies the earlier ADR as superseded.

### 3.3 Requests for Comments (RFCs)

RFCs are used for substantial proposals that need structured discussion before a decision is made. An RFC remains a proposal until the founder records an outcome. Accepted RFCs should lead to updates to the relevant specifications and, where appropriate, an ADR.

### 3.4 Development documentation

Development documentation covers contributor workflows, repository practices, coding standards, and other engineering processes.

## 4. Approval authority

The founder is the final approval authority for:

- Architecture specifications and normative technical requirements.
- Acceptance, rejection, or withdrawal of RFCs.
- Architectural decisions recorded in ADRs.
- Changes that materially alter an accepted architectural direction.

Contributors and maintainers may provide reviews, identify defects, and recommend changes. Review comments do not independently constitute architectural approval.

The author of a change must not infer approval from silence, implementation activity, or a draft being published for review.

## 5. Publication workflow

All documentation changes intended for the default branch must use a pull request.

1. Create a focused branch for the documentation change.
2. Draft or revise the relevant files on that branch.
3. Open a pull request describing the purpose, scope, affected documents, and unresolved questions.
4. Review technical accuracy, consistency, links, status, and compatibility with existing decisions.
5. Obtain explicit founder approval for changes requiring architectural approval.
6. Merge the pull request after approval.

Draft pull requests may be used when early review is useful. A draft PR is not an approval.

Direct commits to the default branch should not be used for routine documentation changes. Exceptional repository administration does not change this policy.

## 6. Document status

Use one of these statuses where applicable:

- **Draft** — under development; not authoritative.
- **Proposed** — submitted for review; not yet approved.
- **Accepted** — approved and currently authoritative.
- **Deprecated** — retained for reference but no longer recommended.
- **Superseded** — replaced by a later document or decision.

A status must reflect an explicit decision, not an assumption.

## 7. Versioning and history

Use stable filenames for living specifications. Do not create parallel files such as `architecture-v0.1.md`, `architecture-v0.2.md`, and `architecture-v0.3.md` for successive edits to the same living document.

Git commits and tags provide revision history. A document-level version field may be used when the specification itself has a defined compatibility or maturity version; it is not a substitute for Git history.

Each specification should identify, at minimum:

- Title.
- Status.
- Document version, if meaningful.
- Last updated date.
- Scope and normative language, where relevant.
- Related specifications and ADRs.

## 8. Maintaining accepted decisions

Do not silently rewrite the rationale of an accepted ADR.

When an accepted decision changes:

1. Write a new ADR explaining the new context and decision.
2. Link to the earlier ADR.
3. Mark the earlier ADR as superseded, identifying the replacing ADR.
4. Update affected architecture specifications in the same change set or in explicitly linked follow-up work.

Superseded documents remain available in Git history and should normally remain in the repository for traceability.

## 9. Consistency with implementation

Implementation and documentation must evolve together. Code does not automatically override an accepted specification.

If implementation work demonstrates that an accepted design is infeasible or incomplete, raise the discrepancy, propose a specification change, and obtain the required approval. Do not silently treat an implementation deviation as a new architectural decision.

## 10. Conversation-to-repository workflow

For work developed with ChatGPT:

1. Explore the problem and alternatives in conversation.
2. Prepare a complete draft in conversation for review.
3. Resolve questions and record any remaining uncertainties explicitly.
4. Obtain the founder's explicit approval.
5. Publish the approved content through a GitHub pull request.
6. Report the PR and its scope; do not merge it without the required approval.

No repository document should be marked accepted merely because a draft was generated or committed to a review branch.

## 11. Related resources

- [Documentation index](../README.md)
- [Architecture index](../architecture/README.md)
- [ADR index](../architecture/decisions/README.md)
- [RFC process](../../rfcs/README.md)
