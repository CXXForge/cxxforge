# ADR-0003: Build Graph and Orchestration Ownership

- **Status:** Accepted
- **Date:** 2026-11-03
- **Decision owners:** Founder
- **Supersedes:** None
- **Superseded by:** None

## Context

C++ projects use a range of build systems and tools. CMake is widely used, but build-system formats and execution behavior differ. CXXForge needs a coherent way to plan builds, understand dependencies, and coordinate execution without making one external build system its canonical architecture.

Implementing a complete native executor immediately could create substantial scope and compatibility risk. Permanently limiting CXXForge to a thin wrapper around existing tools could prevent it from developing an independent build model.

## Decision

CXXForge will own its canonical build graph, action model, planning, and orchestration semantics.

Initially, the build engine will use a **hybrid execution strategy**:
- CXXForge constructs and manages its build graph.
- CXXForge plans actions, dependencies, and execution order.
- Adapters invoke external build systems and tools to perform actual work.
- CMake is an integration adapter, not the canonical CXXForge build model.

The long-term execution strategy is intentionally deferred. A native action executor, continued external execution, or a more granular hybrid may be selected later based on evidence concerning performance, portability, integration fidelity, debuggability, and maintenance cost.

## Alternatives considered

### Permanent wrapper around external build systems

Not selected as a binding long-term decision because it could constrain CXXForge's independent build semantics and future capabilities. External execution remains the initial strategy.

### Immediate native build executor

Not selected for the initial implementation because the scope and compatibility burden are not yet justified.

### CXXForge-owned model with hybrid execution

Selected because it establishes ownership of planning and orchestration while preserving practical interoperability and deferring the expensive execution decision.

## Consequences

### Positive

- CXXForge can define consistent build planning semantics.
- Existing build systems and tools remain usable.
- The project avoids committing prematurely to a complete native executor.
- Execution backends can evolve behind adapters.

### Negative / trade-offs

- Mapping CXXForge actions to external systems may be imperfect.
- Backend-specific behavior can complicate diagnostics and reproducibility.
- The hybrid model introduces adapter and orchestration complexity.

### Risks and mitigations

- **Risk:** External backends expose semantics that cannot be represented accurately.  
  **Mitigation:** Define adapter capability contracts and surface limitations.
- **Risk:** The build engine becomes coupled to one backend.  
  **Mitigation:** Keep the canonical graph and action model independent of backend-specific formats.

## References

- [System Architecture Overview](../system-overview.md)
