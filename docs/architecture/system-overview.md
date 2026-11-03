# CXXForge System Architecture Overview

- **Status:** Accepted
- **Document version:** 0.1
- **Last updated:** 2026-11-03
- **Implementation language:** Rust (proposed)
- **Target ecosystem:** C++
- **Application architecture:** Modular monolith
- **Package strategy:** Independent core with ecosystem adapters
- **Build strategy:** CXXForge-owned build model and orchestration; execution strategy initially hybrid
- **Deployment strategy:** Local-first with optional remote services
- **Platform strategy:** Cross-platform architecture with staged validation

## 1. Purpose and scope

This document establishes the initial high-level architecture for CXXForge. It defines the product boundary, architectural principles, major logical subsystems, ownership of core models, and the intended evolution path.

It is an architectural overview, not a complete specification of package manifests, dependency resolution, lockfiles, build actions, toolchain discovery, ABI compatibility, artifacts, caches, or registries. Those subjects will be specified in focused documents listed in the [architecture register](README.md).

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as normative requirements when written in uppercase.

## 2. Product vision

CXXForge is modern C++ package management, build orchestration, and distribution infrastructure. It aims to provide a coherent workflow for describing C++ projects, resolving dependencies, planning builds, selecting toolchains and targets, producing artifacts, and distributing or reusing those artifacts.

CXXForge will own the canonical semantics of its package and build models. It will interoperate with established C++ tools and package ecosystems through explicit adapters rather than making one external ecosystem the source of truth for all CXXForge behavior.

The initial product is local-first. A developer should be able to use local workflows without depending on a CXXForge-hosted control plane when all required inputs are available locally. Remote registries, artifact repositories, shared caches, authentication services, and remote execution can extend that workflow.

## 3. Goals

- Provide a coherent package and dependency model for C++ projects.
- Provide a build graph and orchestration model independent of any one build backend.
- Integrate with existing compilers, toolchains, build systems, and package ecosystems.
- Represent host, target, toolchain, and ABI-relevant properties explicitly.
- Support reproducible dependency resolution and build planning.
- Track artifact identity and integrity, with provenance capabilities developed over time.
- Support local development first and optional remote infrastructure.
- Establish a cross-platform architecture for Linux, Windows, and macOS.

## 4. Non-goals for the initial architecture

The initial architecture does not require:

- Replacing every existing C++ build system.
- Implementing a native compiler or linker.
- Reimplementing every feature of Conan, vcpkg, or system package managers.
- Operating a mandatory hosted service for local package and build workflows.
- Delivering identical feature parity across all operating systems on day one.
- Distributed or remote build execution in the first implementation.
- A microservices deployment model.

These are boundaries for the initial direction, not permanent prohibitions. Changes of this scale require explicit evaluation and, where appropriate, an RFC and ADR.

## 5. Architectural principles

### AP-01 — Independent package model

CXXForge MUST define its own canonical package identity, dependency semantics, manifest model, and lockfile semantics. External package ecosystems are integrated through adapters.

### AP-02 — Independent build orchestration

CXXForge MUST own its build graph, action model, planning, and orchestration semantics. It MAY delegate action execution to external tools and build systems.

### AP-03 — Interoperability first

CXXForge SHOULD integrate with existing compilers, linkers, build systems, package managers, and development tools where practical. Integration boundaries and limitations MUST be explicit.

### AP-04 — Reproducibility by design

Dependency resolution and build planning SHOULD be deterministic from declared inputs. The system SHOULD capture relevant toolchain, target, configuration, and environment information to support repeatability.

### AP-05 — ABI awareness

CXXForge MUST treat binary compatibility as an explicit concern. Package and artifact compatibility cannot be inferred from a package name and version alone.

### AP-06 — Modular architecture

The implementation SHOULD preserve clear subsystem boundaries, stable internal interfaces, and controlled dependency directions. The initial deployment architecture is a modular monolith.

### AP-07 — Security by design

The architecture SHOULD support integrity verification, provenance, credential isolation, safe handling of untrusted package inputs, and controlled execution boundaries. Detailed security requirements belong in a dedicated specification.

### AP-08 — Incremental evolution

The architecture SHOULD allow capabilities to be introduced incrementally without requiring a redesign of the core package and build models.

### AP-09 — Canonical model ownership

CXXForge-owned models and semantics are authoritative within CXXForge. Adapters translate to and from external systems where a well-defined mapping exists.

### AP-10 — Explicit adapter capabilities

Adapters MUST declare or document supported operations, semantic gaps, lossy translations, and unsupported features. CXXForge MUST NOT imply that incompatible ecosystem concepts are perfectly interchangeable.

### AP-11 — Local-first operation

Core local workflows SHOULD operate without a mandatory remote CXXForge service when all required inputs are available locally. Remote capabilities are optional extensions.

## 6. Logical architecture

The system is organized into the following logical subsystems. These are architectural responsibilities, not a requirement that each subsystem be an independently deployable service or Rust crate.

### 6.1 Developer interface

Provides command-line and, potentially, future graphical or editor-facing interfaces. It accepts user intent, presents plans and diagnostics, and coordinates application workflows through internal interfaces. User-interface concerns SHOULD NOT own package resolution or build semantics.

### 6.2 Workspace and project management

Discovers and manages CXXForge workspaces, project configuration, source roots, profiles, and workspace-level operations. It connects project intent to package and build workflows.

### 6.3 Package engine

Owns package identity, versions, dependency declarations, dependency graph construction, resolution, source selection, and lockfile semantics. It provides the canonical dependency graph consumed by downstream planning.

### 6.4 Build engine

Owns the build graph, action descriptions, dependency ordering, planning, invalidation semantics, and orchestration. Initially, execution is hybrid: CXXForge plans and coordinates work while adapters invoke external tools and build systems. Whether CXXForge later implements a native action executor or retains external execution as a long-term strategy remains an evidence-based decision.

### 6.5 Toolchain engine

Models and discovers compilers, linkers, build tools, SDKs, target triples, platform capabilities, and relevant toolchain properties. It supplies normalized toolchain and target information to planning and compatibility checks.

### 6.6 Artifact engine

Defines artifact identity and metadata, manages local artifact storage, and provides integrity and cache interfaces. Remote artifact storage and shared caching can be added through service integrations.

### 6.7 Integration layer

Contains adapters for external package ecosystems, build systems, compilers, linkers, system tools, and other infrastructure. Adapters isolate external formats and behavior from the canonical CXXForge domain model.

### 6.8 Registry infrastructure

Provides interfaces and implementations for package metadata and distribution services. The architecture permits local sources and optional remote registries. Authentication, authorization, publication, and registry trust policies will be detailed in a dedicated specification.

## 7. Package ecosystem strategy

CXXForge will use an independent core with adapters.

CXXForge owns:
- Canonical package identity and version semantics.
- Dependency declarations and resolution semantics.
- Its manifest and lockfile formats.
- The resolved dependency graph used by its own build planner.

Adapters may integrate with:
- Conan.
- vcpkg.
- pkg-config and system-provided packages.
- Git-based sources.
- Local path sources.
- Other package and distribution systems as justified.

An adapter is a compatibility boundary, not a guarantee of complete semantic equivalence. Each adapter MUST make capability coverage and translation limitations visible. The detailed package model and adapter contracts will be specified separately.

## 8. Build ownership and execution strategy

CXXForge owns the abstract build model: build graph, actions, planning, ordering, and orchestration. External build systems and tools are execution backends during the initial implementation.

CMake is an important integration target, but it is an adapter rather than the canonical CXXForge build model. Other backends may be integrated as requirements and evidence justify.

The architecture deliberately leaves open whether CXXForge should eventually provide native action execution, retain external execution, or use a more granular hybrid. This decision should be informed by integration quality, performance, portability, debuggability, and maintenance cost. It MUST NOT be assumed by this overview.

## 9. Deployment and connectivity

CXXForge is local-first with optional remote services.

Local workflows SHOULD be available without a hosted CXXForge service when required inputs are present locally. Such inputs may include source code, manifests, lockfiles, toolchains, dependencies, and cached artifacts.

Remote services MAY provide:
- Package registries and metadata.
- Artifact distribution.
- Shared or remote caches.
- Authentication and authorization.
- Remote build execution.
- Team collaboration and policy services.

Offline operation is conditional: CXXForge can operate offline only to the extent that all required inputs and services for the requested operation are available locally. The system MUST communicate when network access or unavailable remote resources are required.

## 10. Platform architecture

Linux, Windows, and macOS are architectural target platforms. The system MUST distinguish:

- **Host platform:** the operating system and architecture on which CXXForge itself runs.
- **Target platform:** the platform for which a package or artifact is being built.
- **Toolchain platform:** the platform and execution environment associated with the compiler and related tools.

Core domain models SHOULD remain platform-neutral. Filesystem operations, process management, environment handling, path conventions, toolchain discovery, and platform-specific integration behavior SHOULD be isolated behind infrastructure abstractions.

The initial primary development and CI platform is a separate implementation decision recorded in [ADR-0006](decisions/0006-primary-development-platform.md). Selecting a primary implementation platform does not narrow the architectural target platforms.

## 11. Internal software architecture

The initial implementation is planned as a Rust modular monolith, organized as a workspace with clear crate and module boundaries.

The modular monolith is intended to:
- Keep deployment and operational complexity low.
- Allow explicit subsystem ownership and interfaces.
- Support independent unit and integration testing of modules.
- Preserve the option to extract components later if real requirements justify it.

The exact crate decomposition, public API boundaries, error model, persistence choices, and concurrency strategy belong to implementation design and subsequent specifications. The architecture does not require one crate per logical subsystem.

## 12. Quality attributes

The architecture prioritizes:

- **Correctness:** dependency and build graph semantics must be explicit and testable.
- **Reproducibility:** declared inputs and relevant execution properties should be captured.
- **Portability:** platform-specific behavior must be isolated.
- **Interoperability:** established C++ tools should be usable through well-defined adapters.
- **Extensibility:** new backends, registries, and toolchains should not require changes throughout the core.
- **Security:** untrusted inputs, credentials, artifacts, and external processes require explicit trust boundaries.
- **Performance:** resolution, planning, and artifact reuse should support incremental operation; performance claims require measurement.
- **Maintainability:** subsystem boundaries and architectural decisions must remain documented.

## 13. Evolution and specification roadmap

The following focused specifications are expected to refine this overview:

1. Package and dependency model.
2. Manifest specification.
3. Lockfile specification.
4. Build architecture.
5. Toolchain and target model.
6. ABI compatibility.
7. Artifact and cache architecture.
8. Registry architecture.
9. Security architecture.

The architecture index tracks their status. A specification may be introduced through a focused proposal and reviewed independently.

## 14. Related architectural decisions

- [ADR-0001: Modular Monolith](decisions/0001-modular-monolith.md)
- [ADR-0002: Independent Package Model with Adapters](decisions/0002-independent-package-model.md)
- [ADR-0003: Build Graph and Orchestration Ownership](decisions/0003-build-orchestration-ownership.md)
- [ADR-0004: Local-First Architecture](decisions/0004-local-first-architecture.md)
- [ADR-0005: Cross-Platform Architecture with Staged Validation](decisions/0005-cross-platform-strategy.md)
- [ADR-0006: Linux as the Primary Development and CI Platform](decisions/0006-primary-development-platform.md)

## 15. Governance

This overview is an accepted initial architectural baseline. Changes that materially alter its accepted direction MUST follow the documentation governance policy and be supported by an ADR or RFC as appropriate. The founder is the final approval authority.
