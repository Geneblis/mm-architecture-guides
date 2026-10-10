# ARCHITECTURE.md — Universal

> **Default:** Pragmatic Modular Monolith + Feature-Based Organization + selective Clean Architecture principles. Apply to any stack; do not force a monolith on genuinely distributed systems.

## How the principles fit together

Modular Monolith defines module ownership and collaboration within a single deployable application. Feature-Based Organization groups code by capability. Clean Architecture defines dependency direction inside boundaries that isolate rules from technical details. They are compatible dimensions, not three mandatory layers.

A feature can be a module in a small project; a larger business module may contain several features. Clear public operations and ownership enforce boundaries, not folder names alone. Keep existing deployment topology and framework-, engine- or host-required paths. Libraries, mods and data-oriented projects can use the relevant principles without becoming deployable monoliths or adopting the example `src/` layout.

This guide applies Clean Architecture principles selectively. When rules are isolated, source dependencies point toward those rules: UI, persistence and engine adapters may depend on them, but isolated rules do not import adapter implementations or framework-specific data types. If a rule must trigger an external operation, use a narrow rule-owned contract, function or callback and wire its implementation at the edge. Direct infrastructure access in a simple feature is an intentional tradeoff, not strict Clean Architecture isolation.

## Core rules

1. **Inspect before changing.** Understand the existing structure, conventions, entry points, and affected features. This guide is not permission for a rewrite.
2. **Organize by capability.** Keep each feature's rules, data, and related adapters close together; split a feature only when responsibilities actually diverge.
3. **Own your internals.** Features expose small public operations or contracts; other features must not manipulate private implementation details.
4. **Control dependencies.** Prefer explicit imports or injected collaborators. Avoid cyclic dependencies, hidden globals, and shared mutable state.
5. **Choose the simplest communication.** Use direct calls for clear relationships; events for genuine notifications to independent consumers. Avoid a universal event bus by default.
6. **Separate policy from machinery where useful.** Keep important domain rules independent of UI, storage, transport, or engine concerns when this improves testing or reuse; enforce inward source dependencies at boundaries declared isolated. Do not require fixed Clean Architecture layers.
7. **Abstract on evidence.** Add an interface, service, repository, adapter, or extra layer only when it solves a real boundary, variation, or testing problem.
8. **Keep `Shared` small.** Put only stable, genuinely reusable utilities there; never use it as a dumping ground or as a backdoor between features.
9. **Avoid premature work.** No speculative plugins, microservices, caches, optimizations, configuration knobs, or frameworks. Measure before optimizing unless constraints are known.
10. **Preserve behavior.** Favor small, coherent changes; refactor nearby code only when needed. Follow existing project-specific requirements over illustrative layouts.

## Suggested shape (not mandatory)

```text
src/
  app/          # startup, composition, integration
  features/     # self-contained capabilities
    feature-a/
    feature-b/
  shared/       # truly cross-cutting primitives
```

## Agent execution protocol

- **Locate:** Find the owning feature and its public contract before editing.
- **Plan:** Make the smallest change with clear inputs, outputs, and ownership.
- **Implement:** Use descriptive names, cohesive functions, explicit error handling, and minimal indirection.
- **Verify:** Run relevant tests/build/lint; check boundary crossings and regressions.
- **Report:** Explain changed files, behavior, remaining risks, and any unrun checks.

**Decision rule:** Prefer the design with the fewest concepts needed to make the next change safe and understandable—not the fewest files, and not the most layers.
