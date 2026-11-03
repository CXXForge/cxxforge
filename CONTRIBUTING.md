# Contributing to CXXForge

Thank you for your interest in CXXForge. We value precise technical discussion, reproducible reports, focused changes, and respectful collaboration.

## Before contributing

- Read the project [README](README.md) and [GOVERNANCE](GOVERNANCE.md).
- Search existing issues and discussions before opening a new one.
- For significant design or specification changes, propose an RFC before implementation.
- For accepted architectural decisions, record the outcome as an ADR.

## Contribution types

We welcome contributions to documentation, specifications, tests, tooling, integrations, and implementation. During the initial architecture phase, documentation and design reviews are especially valuable.

## Workflow

1. Open or identify an issue describing the problem or proposal.
2. Discuss scope and acceptance criteria before large changes.
3. Create a focused branch from `main`.
4. Make the smallest coherent change that solves the problem.
5. Add or update tests and documentation where applicable.
6. Run the relevant formatting, linting, and test commands.
7. Open a pull request using the repository template.

Do not combine unrelated refactors, formatting changes, and feature work in one pull request.

## Rust standards

The implementation is planned in Rust. The project intends to use the Rust 2024 edition, with a minimum supported Rust version (MSRV) to be established by the architecture and CI configuration.

When Rust code is introduced:

- Run `cargo fmt --all -- --check`.
- Run `cargo clippy --workspace --all-targets --all-features -- -D warnings` where supported.
- Run relevant unit and integration tests.
- Avoid unnecessary `unsafe`; document and justify any use.
- Return contextual errors and avoid silently discarding failures.
- Document public APIs and non-obvious invariants.

The exact commands may evolve as the workspace is established. Follow the repository's current CI configuration.

## Design and compatibility

- Do not introduce public package-format or protocol changes without the required design process.
- Treat reproducibility, security, and cross-platform behavior as design requirements.
- Do not assume that compiler-version equality proves binary compatibility.
- Preserve interoperability with existing C++ tooling where practical.
- Document platform-specific limitations and test them when possible.

## Pull request expectations

A pull request should explain:

- What changed and why.
- The issue or RFC it addresses.
- Design decisions and alternatives, when relevant.
- Tests performed and their results.
- Compatibility, migration, security, or performance implications.
- Follow-up work that is intentionally out of scope.

A maintainer may request changes, additional tests, or a design discussion before merging.

## Community

Be constructive and respectful. Follow the [Code of Conduct](CODE_OF_CONDUCT.md).

For security vulnerabilities, do not open a public issue. Follow [SECURITY.md](SECURITY.md).
