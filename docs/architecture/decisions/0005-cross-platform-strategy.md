# ADR-0005: Cross-Platform Architecture with Staged Validation

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

CXXForge is intended to serve C++ developers using Linux, Windows, and macOS. These platforms differ in filesystem behavior, process management, environment conventions, toolchain discovery, executable formats, and available system facilities.

Architectural support for multiple platforms does not require implementing and validating every platform with equal priority from the first development iteration. The project needs to preserve portability while allowing implementation and CI coverage to mature in stages.

The selection of a primary development and CI platform is a separate operational decision and should not be conflated with the intended platform scope.

## Decision

CXXForge will adopt a **cross-platform architecture with staged implementation and validation**.

1. Linux, Windows, and macOS are architectural target platforms.
2. Core domain models and business logic MUST remain platform-independent wherever practical.
3. Platform-specific operations MUST be isolated behind infrastructure interfaces and adapters.
4. The architecture MUST distinguish host platform, target platform, and toolchain platform.
5. Platform-specific capabilities and limitations MUST be explicit.
6. The initial primary development and CI platform is determined separately by ADR-0006.

This ADR establishes architectural scope. It does not require simultaneous feature parity or equal CI coverage across all three operating systems.

## Alternatives considered

### Linux-only architecture

Rejected because it would constrain the intended audience and make later portability substantially more expensive.

### Full simultaneous validation on all platforms from the first iteration

Not selected because it could impose disproportionate initial CI and implementation overhead before core workflows stabilize.

### Cross-platform architecture with staged validation

Selected because it preserves portability as a design constraint while allowing practical prioritization.

## Consequences

### Positive

- Platform portability is considered from the beginning.
- Platform-specific behavior has explicit architectural boundaries.
- Implementation and CI coverage can expand incrementally.
- Host, target, and toolchain concepts remain distinct.

### Negative / trade-offs

- Abstractions may need refinement as real platform differences emerge.
- Staged validation can allow platform-specific defects to remain undetected until a platform enters active CI coverage.
- Maintaining multiple platform adapters increases long-term testing and maintenance work.

### Risks and mitigations

- **Risk:** Linux assumptions leak into core logic.  
  **Mitigation:** Isolate operating-system behavior and add cross-platform tests as platform coverage expands.
- **Risk:** Architectural portability is claimed without practical validation.  
  **Mitigation:** Track platform validation status explicitly and avoid claiming support beyond tested capabilities.

## References

- [System Architecture Overview](../system-overview.md)
- [ADR-0006: Linux as the Primary Development and CI Platform](0006-primary-development-platform.md)
