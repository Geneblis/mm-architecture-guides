# Consistency review

Document review conducted on October 9, 2026, covering all eight guides, the README, and the adoption prompt.

## Result

The guides are compatible as a catalogue of **Modular Monolith, Feature-Based Organization, and selective Clean Architecture principles**. These concepts address different dimensions and can be used together. The catalogue does not prescribe a complete, mandatory implementation of Clean Architecture.

Dependency direction is the deciding factor: when a rule is described as independent of UI, a database, or an engine, it must not import those details. Dividing files into folders without respecting that rule does not create the stated isolation. Simple projects can have smaller boundaries and access infrastructure directly, provided that choice is described accurately.

## Guides examined

| Guide | Assessment |
| --- | --- |
| Universal | Consistent baseline of boundaries, explicit dependencies, and justified abstractions. It now distinguishes the three dimensions, defines dependency direction at isolated boundaries, and preserves environment-required structures. |
| API | Consistent feature organization and module contracts. Direct ORM access was scoped to avoid contradicting rule isolation. It does not require CQRS, events, or generic repositories. |
| Web | Consistent with framework routes and conventions; separates browser and server code and keeps complex rules outside the UI when necessary. |
| Desktop | Consistent with features, operating-system boundaries, UI-thread constraints, cancellation, and existing persistence. |
| Mobile | Consistent with features and lifecycle. Token guidance was corrected: sessions may require client-side tokens protected by platform secure storage. Privileged secrets and authorization decisions remain server-side. |
| CLI | Consistent for small tools; does not require layers and preserves arguments, output, and exit codes. |
| Unity | Consistent with engine composition and lifecycle; separation of C# rules is selective. Preserves scenes, prefabs, GUIDs, and serialized data. |
| Unreal | Consistent with Actors, Components, Subsystems, C++, and Blueprints; does not turn every feature into an engine plugin or module. Preserves references and serialization. |

## Corrections made

- The README changed from a single-guide selection instruction to a catalogue with component-level selection, usage examples, a description, and clear limitations.
- The prompt now uses the link or path supplied by the user instead of pointing to a fictional account.
- Projects spanning several environments can combine guides, with separate scope for each component.
- Adoption preserves existing local documents and records the source and consulted revision when available.
- The workflow distinguishes reading a temporary clone, copying guidelines, and adapting a structure to the project.
- Implementation continues within the already authorized request; the documentation does not add a mandatory approval step for every structural edit.
- The catalogue does not install skills or assume every agent automatically reads `ARCHITECTURE.md`.

## Scenarios examined

This table records an analysis of the instructions, without executing an independent agent or real applications.

| Scenario | Expected workflow behavior |
| --- | --- |
| Web application with its own API | Universal + Web + API, with boundaries and decisions for each component. |
| CLI with a few commands | Universal + CLI; necessary functions and folders without artificial layers. |
| Existing Unity project | Universal + Unity; local changes that preserve assets and references. |
| Services already deployed separately | Preserve topology; apply modularity and rule separation within the affected component. |
| Mod with game-required directories | Universal; respect host paths instead of imposing `src/features/`. |
| Project with its own `ARCHITECTURE.md` | Read and incorporate only relevant guidelines, preserving local decisions and adaptations. |
| Adoption-only request | Produce documentation and useful structure; finish without inventing product code. |
| Remote guides unavailable | Use a supplied local copy or report missing access; do not claim remote files were read. |

## Conceptual references

- [The Clean Architecture — Robert C. Martin](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html): dependency direction, independent rules, and boundaries between policies and technical details.
- [Modular Monolith with DDD — Kamil Grzybek](https://github.com/kgrzybek/modular-monolith-with-ddd): a concrete modular-monolith example with internal separation. This catalogue does not require additional patterns used by that example, such as DDD or CQRS.

## Verification limits

Completed checks: presence of all eight guides, resolution of the 21 local Markdown links, closed code fences, absence of the fictional address and personal paths in the documents, and preservation of the license and five guides that did not require changes. Files saved in the destination folder were compared by hash with the reviewed version.

The review covers guideline consistency and document navigation. It does not prove that every LLM will follow the workflow or replace compilation, tests, and verification of the target project after code changes. No remote publication occurred during this preparation.
