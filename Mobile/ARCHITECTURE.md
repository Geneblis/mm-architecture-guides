# ARCHITECTURE.md — Mobile Applications

> **Default:** Feature-based Modular Monolith adapted to the platform (Android, iOS, Flutter, React Native, etc.).

## Principles

1. Inspect navigation, screen lifecycle, state management, persistence, build targets, and platform conventions before changes.
2. Group screens, state, rules, and data integrations by user-facing feature; avoid one giant `screens/` or `services/` dumping ground.
3. Keep UI views focused on interaction and presentation; separate complex reusable rules only when justified.
4. Expose narrow feature operations; avoid cross-feature access to private state and hidden global mutable stores.
5. Prefer platform/framework-native navigation, async patterns, and dependency management over custom abstractions.
6. Respect lifecycle changes, background/foreground transitions, permissions, cancellation, memory limits, and offline behavior **as applicable**.
7. Keep privileged secrets and authorization decisions server-side. Protect necessary client session tokens with platform secure storage, preserve the established authentication flow, and validate device inputs and network responses at the relevant boundaries.
8. Share components only after actual reuse; do not split features into packages or layers simply for architectural symmetry.
9. Introduce caching, sync engines, repositories, and event buses only when current requirements demand them.
10. Preserve stored user data, deep links, navigation behavior, and platform compatibility during refactors.

## Suggested layout (adapt to framework)

```text
src/
  app/                    # startup, navigation, global composition
  features/
    profile/
    messaging/
    settings/
  platform/               # device-specific adapters when needed
  shared/                 # genuinely reusable components/helpers
```

## Agent workflow

- Identify the owning feature, screen lifecycle, network/data flow, and permission boundaries.
- Make the smallest coherent change, respecting existing platform architecture.
- Verify build, relevant tests, navigation, accessibility, and target-device behavior when possible.
- State what was not tested on real devices or operating systems.

**Boundary test:** A messaging update should not require modifying profile internals.
