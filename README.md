# CXXForge

**Modern C++ package management, build orchestration, and distribution infrastructure.**

CXXForge is an open-source project exploring a unified development ecosystem for modern C++. Its long-term goal is to make creating, building, testing, packaging, and distributing C++ software substantially more coherent and reproducible.

> **Project status:** Early-stage project. The repository is establishing its specifications, architecture, and engineering foundations. No production-ready package manager or build engine is available yet.

## Vision

CXXForge aims to bring together:

- **Package management:** deterministic dependency resolution, manifests, lockfiles, registries, and package publishing.
- **Build infrastructure:** a declarative build graph, incremental execution, compiler integration, and eventually a native build engine.
- **Binary distribution:** toolchain-aware artifacts, compatibility policies, content-addressable storage, and caching.
- **Toolchains and targets:** compiler discovery, target profiles, SDK integration, and cross-compilation.
- **Security and supply chain:** package integrity, provenance, vulnerability reporting, and auditable builds.

The project will be implemented primarily in **Rust** and will manage projects written in **C++**.

## Architectural principles

1. **Independent core:** package and build models belong to CXXForge. Existing build systems are integrations, not the permanent internal architecture.
2. **Interoperability:** support existing C++ projects and workflows rather than requiring immediate migration.
3. **Reproducibility:** dependency resolution and build execution should be deterministic wherever the inputs permit it.
4. **Conservative binary compatibility:** matching compiler labels alone must never be treated as proof of ABI compatibility.
5. **Cross-platform design:** platform and toolchain differences are explicit parts of the model.
6. **Incremental delivery:** each release should be useful without compromising the long-term architecture.
7. **Open specifications:** package formats and important protocols should be documented independently of implementation details.

## Development status

The current priority is to define the architecture and public specifications before committing to implementation details. Planned areas include package identity, manifests, lockfiles, dependency resolution, build actions, toolchains, ABI policy, artifact storage, and registry protocols.

See [the roadmap](ROADMAP.md) when available, and the [architecture decision records](docs/architecture/decisions/README.md).

## Contributing

CXXForge welcomes thoughtful discussion and, as the project matures, code and documentation contributions. Please read [CONTRIBUTING.md](CONTRIBUTING.md), [GOVERNANCE.md](GOVERNANCE.md), and [SECURITY.md](SECURITY.md) before contributing.

For substantial architectural or specification changes, use the RFC process described in [rfcs/README.md](rfcs/README.md).

## License

CXXForge is intended to be distributed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for the authoritative license text.
