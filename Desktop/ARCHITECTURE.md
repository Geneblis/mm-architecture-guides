# ARCHITECTURE.md — Desktop Applications

> **Default:** Feature-based Modular Monolith; keep application rules distinct from OS/UI framework interactions where valuable.

## Principles

1. Inspect the existing toolkit (Qt, WPF, WinUI, Avalonia, Electron, Tauri, etc.), packaging, persistence, and platform targets.
2. Group related screens, workflows, state, and models by feature; do not scatter one feature across generic `Views/`, `Services/`, and `Models/` trees without reason.
3. Keep UI views focused on rendering and user interaction; move complicated rules to feature-owned logic that can be tested independently.
4. Confine filesystem, OS APIs, native integrations, and inter-process communication to explicit boundaries when they add complexity or security risk.
5. Manage UI-thread affinity, background tasks, cancellation, and resource disposal with the framework's actual lifecycle.
6. Define small public contracts between features; avoid hidden global state, god view-models, and all-purpose controllers.
7. Prefer direct calls where relationships are clear; use events for genuinely independent UI updates, not every method call.
8. Reuse the established persistence/configuration system; protect compatibility with existing user data and migrations.
9. Add interfaces/adapters only for meaningful platform differences, substitutes, or tests. Avoid needless MVVM/MVC/DDD ceremony if the application is simple.
10. Profile startup, memory, and responsiveness before optimizing; prioritize correctness and understandable async behavior.

## Suggested layout (illustrative)

```text
src/
  App/                    # startup, window wiring, composition
  Features/
    Documents/            # view + workflow + logic
    Search/
    Preferences/
  Platform/               # OS/framework-specific integrations
  Shared/                 # narrowly reusable utilities
```

## Agent workflow

- Identify the owning feature and its UI-thread, persistence, and platform constraints first.
- Make a focused change without replacing the app's established architectural pattern.
- Verify compilation, UI behavior, async cancellation, data compatibility, and packaging when possible.
- Report untested platforms or native dependencies explicitly.

**Boundary test:** Editing a document workflow should not require manipulating the internals of preferences or OS adapters.
