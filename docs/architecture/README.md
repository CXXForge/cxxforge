# CXXForge Architecture

This directory is the canonical home for accepted architecture specifications and their working drafts.

## Architecture baseline

The initial system architecture has been explored in the project planning process, but the resulting Architecture Specification v0.1 has not yet been approved or published as an authoritative specification. Its content will be decomposed into focused documents and reviewed individually.

## Specification register

The following documents are planned. Their presence in this register does not mean they have been approved.

| Specification | Status | Scope |
|---|---|---|
| [System overview](system-overview.md) | Planned | Product boundaries, logical subsystems, principles, and high-level architecture |
| [Package and dependency model](package-model.md) | Planned | Package identity, versions, dependency sources, resolution, and features |
| [Manifest specification](manifest-specification.md) | Planned | Manifest syntax and semantics |
| [Lockfile specification](lockfile-specification.md) | Planned | Resolved dependency graph and reproducibility |
| [Build architecture](build-architecture.md) | Planned | Build graph, actions, execution, and incremental behavior |
| [Toolchain and target model](toolchain-model.md) | Planned | Compilers, toolchains, platforms, and target descriptions |
| [ABI compatibility](abi-compatibility.md) | Planned | Binary compatibility profiles and compatibility decisions |
| [Artifact and cache architecture](artifact-and-cache.md) | Planned | Artifact identity, storage, integrity, and cache reuse |
| [Registry architecture](registry-architecture.md) | Planned | Registry metadata, publishing, distribution, and authentication |
| [Security architecture](security-architecture.md) | Planned | Integrity, provenance, auditing, and build isolation |

## Architectural decisions

Accepted and superseded architectural decisions are recorded as individual [Architecture Decision Records](decisions/README.md).

## Change policy

Specifications are drafted and reviewed before publication. The founder is the approval authority. Changes intended for the default branch are submitted through pull requests. Significant changes to accepted architectural decisions must be recorded in an ADR; substantial proposed changes may first be developed as RFCs.

See the [documentation governance policy](../development/documentation-governance.md).
