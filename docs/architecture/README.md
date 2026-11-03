# CXXForge Architecture

This directory is the canonical home for accepted architecture specifications and their working drafts.

## Architecture baseline

The [System Architecture Overview](system-overview.md) is the accepted initial architectural baseline (version 0.1). It establishes CXXForge's product boundaries, architectural principles, logical subsystems, and initial strategic direction.

The overview is intentionally high-level. Focused specifications will define package semantics, manifests, lockfiles, build behavior, toolchains, ABI compatibility, artifacts, registries, and security in greater detail.

## Specification register

The following documents are planned or maintained. Status indicates whether a document is an approved specification.

| Specification | Status | Scope |
|---|---|---|
| [System overview](system-overview.md) | Accepted v0.1 | Product boundaries, logical subsystems, principles, and high-level architecture |
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

The initial architectural baseline is supported by six accepted [Architecture Decision Records](decisions/README.md). Later changes to accepted decisions must be recorded through new ADRs rather than silently rewriting decision history.

## Change policy

Specifications are drafted and reviewed before publication. The founder is the approval authority. Changes intended for the default branch are submitted through pull requests. Significant changes to accepted architectural decisions must be recorded in an ADR; substantial proposed changes may first be developed as RFCs.

See the [documentation governance policy](../development/documentation-governance.md).
