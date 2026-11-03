# ADR-0002: Independent Package Model with Adapters

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

The C++ ecosystem contains established package and dependency-management systems, including Conan, vcpkg, and system package managers. Their concepts, metadata, resolution behavior, and feature sets are not identical.

Delegating all package semantics to one existing ecosystem would constrain CXXForge's capabilities and make its behavior dependent on an external system's model. Building an entirely isolated ecosystem, however, would discard useful existing packages and workflows.

CXXForge needs a canonical model while remaining interoperable with existing tools and sources.

## Decision

CXXForge will own an independent canonical package model and integrate external ecosystems through explicit adapters.

CXXForge owns the semantics of:
- Package identity and versioning within CXXForge.
- Dependency declarations and resolution.
- Its manifest and lockfile formats.
- The canonical resolved dependency graph consumed by its build engine.

Adapters MAY integrate with Conan, vcpkg, pkg-config, system packages, Git sources, local path sources, and additional ecosystems as justified.

Each adapter MUST document:
- The external operations and metadata it supports.
- How external concepts map to CXXForge concepts.
- Unsupported features and semantic gaps.
- Whether any translation is lossy or changes behavior.
- Relevant limitations and operational requirements.

CXXForge MUST NOT imply complete semantic equivalence where an adapter cannot preserve the meaning of the source ecosystem.

## Alternatives considered

### Delegate package management to a single external ecosystem

Rejected because it would make CXXForge's core semantics subordinate to one ecosystem and limit its ability to provide a consistent package model.

### Build an isolated package ecosystem without adapters

Rejected because it would unnecessarily reduce interoperability and make adoption harder for projects already using established tools.

### Independent core with adapters

Selected because it provides ownership of core semantics while allowing incremental integration with existing ecosystems.

## Consequences

### Positive

- CXXForge can evolve its package model independently.
- Existing package sources and workflows can be integrated incrementally.
- Adapter boundaries make compatibility limitations explicit.
- The canonical dependency graph can be consumed consistently by CXXForge's build engine.

### Negative / trade-offs

- CXXForge must implement and maintain its own package semantics.
- Adapters require ongoing compatibility work.
- Some external features may not map cleanly into the canonical model.

### Risks and mitigations

- **Risk:** Adapter behavior gives users a false impression of equivalence.  
  **Mitigation:** Publish capability matrices and surface unsupported or lossy mappings.
- **Risk:** The canonical model becomes too narrow or too complex.  
  **Mitigation:** Evolve it through focused specifications and RFCs informed by real package use cases.

## References

- [System Architecture Overview](../system-overview.md)
