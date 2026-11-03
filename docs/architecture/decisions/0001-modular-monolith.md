# ADR-0001: Modular Monolith

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

CXXForge spans several substantial responsibilities: package management, dependency resolution, build orchestration, toolchain integration, artifact handling, and registry connectivity. These responsibilities require clear boundaries, but the project does not initially need independently deployed services.

A distributed service architecture would introduce network contracts, deployment automation, service discovery, operational monitoring, and failure modes before there is evidence that independent deployment is necessary. At the other extreme, a single undifferentiated codebase would make ownership and dependency boundaries difficult to maintain.

The implementation is planned in Rust, whose workspace and crate model can support explicit internal boundaries.

## Decision

CXXForge will initially be implemented as a **modular monolith**, organized as a Rust workspace.

The implementation MUST:
- Maintain explicit boundaries between major responsibilities.
- Define controlled dependency directions between modules and crates.
- Keep domain semantics separate from operating-system and external-tool integration details.
- Expose internal interfaces deliberately rather than relying on unrestricted cross-module access.
- Support focused unit and integration testing at subsystem boundaries.

The logical subsystems in the system overview do not mandate a one-to-one mapping to Rust crates. Crate decomposition is an implementation-design decision.

Independent deployment or extraction of components may be considered later when justified by concrete scaling, reliability, security, or team-ownership requirements.

## Alternatives considered

### Microservices from the beginning

Rejected for the initial architecture because the operational and distributed-systems overhead is not justified before subsystem boundaries and usage patterns are understood.

### One large, unstructured application

Rejected because it provides insufficient architectural constraints as package, build, toolchain, and artifact responsibilities grow.

### Modular monolith

Selected because it combines explicit internal boundaries with a simple initial deployment and development model.

## Consequences

### Positive

- Lower initial operational complexity.
- Clearer subsystem ownership and test boundaries.
- Easier refactoring while domain models are evolving.
- Preserves the option of future component extraction.

### Negative / trade-offs

- Module boundaries require discipline and review.
- A shared release and deployment unit may eventually constrain independent scaling or release cadence.
- Poorly controlled dependencies could erode modularity over time.

### Risks and mitigations

- **Risk:** The monolith becomes tightly coupled.  
  **Mitigation:** Review dependency direction, keep interfaces explicit, and test important boundaries.
- **Risk:** Premature crate fragmentation increases complexity.  
  **Mitigation:** Let actual cohesion and dependency needs guide crate boundaries.

## References

- [System Architecture Overview](../system-overview.md)
