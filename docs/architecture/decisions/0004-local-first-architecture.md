# ADR-0004: Local-First Architecture

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

CXXForge is intended for developer workstations and potentially team and CI environments. A server-centric design would make local workflows dependent on service availability, connectivity, and hosted infrastructure. A completely local-only design would make future shared registries, artifact distribution, remote caching, and collaboration difficult to introduce.

The architecture should support local development as a first-class workflow while allowing remote capabilities to extend it.

## Decision

CXXForge will adopt a **local-first architecture with optional remote services**.

Core local workflows SHOULD operate without a mandatory hosted CXXForge service when all required inputs are available locally.

Remote services MAY provide:
- Package registries and metadata.
- Artifact repositories and distribution.
- Shared or remote caches.
- Authentication and authorization.
- Remote build execution.
- Team collaboration and policy services.

Offline operation is conditional. An operation can complete offline only when all required source inputs, dependencies, toolchains, metadata, and artifacts are available locally. CXXForge MUST report when a requested operation requires an unavailable remote resource.

## Alternatives considered

### Server-centric architecture

Rejected for the initial architecture because it would make ordinary local workflows depend on remote service availability and connectivity.

### Fully local architecture

Not selected because it would make future shared infrastructure and team capabilities harder to integrate.

### Local-first with optional remote services

Selected because it supports independent local workflows without precluding remote capabilities.

## Consequences

### Positive

- Local development is not inherently coupled to a hosted control plane.
- Remote services can be adopted incrementally.
- Offline workflows are possible when inputs are cached or otherwise available.
- The same core concepts can serve developer workstations and CI environments.

### Negative / trade-offs

- Local and remote resource behavior must be modeled consistently.
- Cache, registry, and authentication boundaries add complexity.
- Offline completeness depends on the availability of all required inputs.

### Risks and mitigations

- **Risk:** Users assume every operation works offline.  
  **Mitigation:** Make network requirements and missing inputs explicit.
- **Risk:** Remote services become implicitly mandatory through implementation shortcuts.  
  **Mitigation:** Test core local workflows without CXXForge-hosted services.

## References

- [System Architecture Overview](../system-overview.md)
