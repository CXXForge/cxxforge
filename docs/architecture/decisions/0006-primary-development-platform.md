# ADR-0006: Linux as the Primary Development and CI Platform

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

CXXForge requires a consistent environment for its initial implementation, development, and continuous integration. Although the architecture targets Linux, Windows, and macOS, equal implementation and CI priority across all three platforms from the outset would increase initial infrastructure and maintenance costs.

Selecting a primary development platform provides a predictable baseline for developer tooling, integration testing, and CI while the core architecture and workflows mature.

This operational priority must not narrow the cross-platform architectural scope established by ADR-0005.

## Decision

**Linux will be the primary development and CI platform during the initial implementation of CXXForge.**

1. Initial development and integration testing will prioritize Linux.
2. The primary CI pipeline will run on Linux.
3. Linux-specific implementation assumptions MUST NOT leak into platform-independent domain logic.
4. Windows and macOS compatibility MUST be considered in architecture and implementation decisions.
5. Additional CI environments for Windows and macOS will be introduced as implementation maturity and project requirements justify them.
6. The specific Linux distribution, version, and support baseline will be determined during implementation planning.

This ADR selects a primary implementation environment; it does not declare Linux the only supported host or target platform.

## Alternatives considered

### Equal development and CI priority across Linux, Windows, and macOS immediately

Not selected for the initial phase because it increases early infrastructure and maintenance costs before core workflows have stabilized.

### A different single primary platform

Not selected. Linux is chosen as the initial baseline for development and CI.

### Linux primary with cross-platform architectural scope

Selected because it provides a focused implementation environment without abandoning Windows and macOS as architectural targets.

## Consequences

### Positive

- A consistent baseline for development and CI.
- Lower initial cross-platform CI complexity.
- Early feedback from Linux integration testing.
- A clear distinction between implementation priority and architectural support scope.

### Negative / trade-offs

- Windows- and macOS-specific defects may be discovered later.
- Some portability issues may require additional rework if not considered during design.
- Linux distribution and version choices remain open until implementation planning.

### Risks and mitigations

- **Risk:** Linux-specific behavior becomes embedded in core abstractions.  
  **Mitigation:** Keep platform-specific operations behind infrastructure boundaries and review portability during design.
- **Risk:** Secondary platforms receive insufficient validation.  
  **Mitigation:** Define measurable platform-enablement milestones and introduce CI coverage as the implementation matures.

## References

- [System Architecture Overview](../system-overview.md)
- [ADR-0005: Cross-Platform Architecture with Staged Validation](0005-cross-platform-strategy.md)
