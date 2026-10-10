# ARCHITECTURE.md — Unreal Engine

> **Default:** Pragmatic Modular Monolith by gameplay feature; integrate through Unreal Actors, Components, Subsystems, data assets, C++, and Blueprints only where they fit.

## Principles

1. Inspect existing `Source/`, `Content/`, project modules, Blueprints, data assets, and engine version before reorganizing anything.
2. Organize gameplay code/assets around features; do not create separate Unreal plugins or engine modules simply to mirror each folder.
3. Use `Actor` for world entities, `ActorComponent` for composable actor behavior, and `Subsystem` only for appropriately scoped services. Avoid all-purpose god Actors/Subsystems.
4. Put reusable gameplay rules in focused C++ classes/functions when valuable; keep Blueprint graphs focused on orchestration and designer-authored behavior where practical.
5. Define narrow public feature operations. Other features should not modify internal actor state or rely on another feature's Blueprint graph structure.
6. Prefer direct calls for known relationships; use delegates/events when multiple independent listeners need notification. Avoid universal messaging infrastructure by default.
7. Respect UObject ownership, garbage collection, reflection (`UPROPERTY`/`UFUNCTION`), asset references, threading, and game-thread constraints.
8. Separate replicated/server-authoritative behavior from purely local presentation **when multiplayer is in scope**; do not add networking layers to single-player projects.
9. Use Data Assets/Data Tables for authored data when they simplify workflows; do not treat them as an excuse for universal indirection.
10. Add interfaces, templates, plugins, managers, and extra layers only for real reuse or dependency boundaries. Measure performance before optimizing.
11. Preserve existing asset paths, Blueprint references, serialization, and packaging/cooking behavior during changes.

## Suggested layout (not a mandated module split)

```text
Source/MyProject/
  Core/                   # startup and integration
  Features/
    Combat/
    Inventory/
    Quests/
  Shared/                 # narrowly reusable code
Content/
  Features/               # associated Blueprints, UI, data assets
```

## Agent workflow

- Identify the owning feature, engine lifecycle, native/Blueprint contract, and affected assets first.
- Change the smallest coherent set of classes/assets; preserve exposed names and Blueprint compatibility.
- Validate builds, editor logs, Blueprint compilation, PIE behavior, and relevant cook/package paths when available.
- State checks not performed; never claim an Unreal project works solely because C++ text looks correct.

**Boundary test:** Features communicate through intentional C++/Blueprint APIs, not by reaching into each other's internal graphs.
