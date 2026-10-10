# ARCHITECTURE.md — Unity

> **Default:** Pragmatic Modular Monolith organized by gameplay feature; composition through Unity components; selective separation of pure C# rules from engine integration.

## Principles

1. Inspect the existing scenes, scripts, prefabs, ScriptableObjects, assembly definitions, and conventions before changing architecture.
2. Group code and related assets by feature (combat, inventory, cities, UI, saving), not into global `Managers/`, `Controllers/`, and `Data/` piles.
3. Keep `MonoBehaviour` focused on lifecycle, scene references, input, and Unity-facing presentation. Put substantial engine-independent rules in plain C# **when useful**.
4. Use `ScriptableObject` for authored definitions/configuration when appropriate; do not accidentally use shared assets as mutable per-save runtime state.
5. Give each feature a clear public API. Other features must not manipulate its private components or serialized state directly.
6. Prefer direct calls for simple collaboration; use C# events for genuine state changes with multiple independent listeners. Subscribe/unsubscribe with the correct Unity lifecycle.
7. Keep dependencies explicit via serialized references, constructors for plain classes, or existing project wiring. Avoid unnecessary service locators and proliferating singletons.
8. Let Unity handle scene, prefab, physics, animation, and asset lifecycles. Do not reimplement engine services without a concrete need.
9. Create interfaces, asmdefs, custom inspectors, factories, or generic frameworks only when they solve a real problem; avoid overmodularizing small features.
10. Preserve prefab/scene references, asset GUIDs (`.meta` files), serialized field compatibility, and existing behavior during refactors.
11. Profile allocations, rendering, physics, and update loops before optimizing; avoid per-frame work only when its cost is evident or clearly unnecessary.

## Suggested layout (adapt to current project)

```text
Assets/
  Scripts/
    Core/                 # startup and composition only
    Features/
      Combat/             # related components, models, logic
      Inventory/
      Notifications/
    Shared/               # proven cross-feature helpers
  Art/  Scenes/  Resources/  # retain established asset conventions
```

## Agent workflow

- Trace the affected feature from trigger to component to data and UI; edit only necessary files.
- Prefer descriptive C# and short comments explaining **why**, not boilerplate patterns.
- Do not introduce a new manager or event bus if an existing API is sufficient.
- Validate compilation, scene/prefab wiring, serialization, and Play Mode behavior when available; state explicitly what was not tested.

**Boundary test:** A change in `Inventory` should not require editing `Combat` internals unless an explicit shared contract genuinely changes.
