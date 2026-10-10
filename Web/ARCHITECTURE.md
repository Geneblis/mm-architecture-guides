# ARCHITECTURE.md — Websites & Web Applications

> **Default:** Feature-based modular application; selective Clean Architecture boundaries; work with the chosen framework and its routing/rendering model.

## Principles

1. Inspect routing, deployment, rendering mode, state management, backend integration, and existing conventions before restructuring.
2. Group feature-specific pages, components, state, validation, and data access together where the framework allows.
3. Keep cross-feature UI primitives in `shared/ui` **only after real reuse**; avoid an enormous global `components/` directory.
4. Distinguish browser code from server-only code. Secrets, privileged operations, and trusted authorization checks belong server-side.
5. Expose narrow feature APIs; do not read or mutate another feature's private stores, hooks, or internal files.
6. Prefer framework-native data fetching, navigation, forms, and caching over custom infrastructure unless requirements justify it.
7. Keep business rules independent of visual components when they are complex, reused, or need isolated tests. Do not force separate layers for trivial pages.
8. Use local state by default; adopt shared state only for genuine cross-feature coordination. Avoid a global store as a catch-all.
9. Validate inputs at trust boundaries; handle loading, empty, failure, and accessibility states as part of the feature.
10. Avoid speculative abstractions, premature memoization, custom design systems, and premature performance work. Measure real bottlenecks.

## Suggested layout (adapt to framework)

```text
src/
  app/                    # routes, root layout, providers, wiring
  features/
    auth/                 # UI + state + integration for auth
    catalog/
    checkout/
  shared/                 # genuinely common UI/utilities
```

## Agent workflow

- Trace route -> feature -> data/state -> UI before editing.
- Change locally; preserve URLs, API contracts, styling conventions, and accessibility.
- Verify type checks, lint, feature tests, build, and relevant desktop/mobile viewport behavior when possible.
- Do not introduce a new state library, router, data layer, or framework for a small feature change.

**Boundary test:** A catalog UI change should not require changes inside authentication internals.
