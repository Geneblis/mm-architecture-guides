# Architecture adoption workflow

Use this process when a user provides this repository as an architecture reference for a development task. These documents guide the requested work; they do not authorize unrelated refactoring, publishing, deployment, or global agent configuration.

## 1. Inspect the target project

Read the target project's applicable instructions and existing architecture decisions. Identify the requested outcome, affected features, framework or engine, entry points, dependency direction, data ownership, deployment topology and relevant compatibility constraints.

For a new project, use the user's chosen stack and requirements. If a missing choice materially affects implementation, ask a focused question while continuing independent work. For an existing project, prefer its established conventions unless a concrete problem requires a change.

## 2. Retrieve and select the references

Read this repository's README and this workflow. Retrieve files through available repository tools, direct file access, or a temporary clone outside the target working tree. Record the source revision when the retrieval method exposes one. Do not claim a revision is known if it is not, or infer access from a URL alone.

Read [Universal](Universal/ARCHITECTURE.md) as the common baseline. Select only the environment guides relevant to the components being changed:

| Component | Reference |
| --- | --- |
| Backend, service or API | [API](API/ARCHITECTURE.md) |
| Website or web application | [Web](Web/ARCHITECTURE.md) |
| Desktop application | [Desktop](Desktop/ARCHITECTURE.md) |
| Mobile application | [Mobile](Mobile/ARCHITECTURE.md) |
| Command-line tool or automation | [CLI](CLI/ARCHITECTURE.md) |
| Unity client or game | [Unity](Unity/ARCHITECTURE.md) |
| Unreal client or game | [Unreal](Unreal/ARCHITECTURE.md) |
| Library, mod, data-oriented project or another environment | [Universal](Universal/ARCHITECTURE.md), adapted to its host constraints |

Apply multiple guides to their respective components when necessary. An Electron application may need Desktop and Web guidance; a Unity client with a backend may need Unity and API. Apply guidance at the component level without collapsing independently deployed services into one monolith.

Choose a suitable design for the current requirements and explain the tradeoff. This catalogue supplies defaults, not evidence that one architecture is universally best.

If the reference is inaccessible, use a local copy supplied by the user or report the missing access. An illustrative directory tree is not an executable template or proof that a build will work.

## 3. Define the adaptation

Briefly explain the selected guides, relevant module boundaries, dependency direction and smallest necessary changes before editing. Within the user's authorized scope, proceed with ordinary adoption and implementation; this workflow does not add a separate approval gate. Clarify decisions that require new scope or conflict with an explicit requirement.

Keep the three dimensions distinct:

- **Modular Monolith:** ownership and collaboration between modules in a single deployable application, where that topology fits.
- **Feature-Based Organization:** grouping code and related resources by capability within the framework's constraints.
- **Selective Clean Architecture:** isolating significant rules from technical details where useful. For any boundary declared isolated, source dependencies point toward those rules. Use a function, callback or narrow interface when a rule must invoke an external effect without importing its implementation.

In a small application, one feature can be one module. Larger modules can contain multiple features. A folder name alone does not enforce a boundary. Cross-module calls use public operations; private tables, state and implementation types stay owned by their module.

Preserve existing distributed topology and engine-, framework- or host-required paths. A library or mod does not need to be described as a deployable monolith. Prefer an incremental adaptation over reorganizing the entire project.

## 4. Incorporate the architecture locally

Create or update the target project's `ARCHITECTURE.md`, or its established equivalent. Include enough adapted guidance to use it without consulting this catalogue for every edit:

- Source repository URL or local path, source revision when known, and selected guide paths.
- The actual project environment and the scope of each selected guide.
- Module or feature ownership, public collaboration points and dependency direction.
- The relevant existing directory layout or the smallest layout being introduced.
- Compatibility constraints, intentional exceptions and applicable validation steps.

If an architecture document already exists, read it and merge only relevant guidance. Preserve project-specific decisions and user edits; copying a guide is not permission to replace them. Resolve conflicts according to the current request and applicable project requirements, and state material tradeoffs.

For one environment, start from the selected guide and add the applicable Universal rules and project decisions. For mixed environments, compose a single document with clear component scopes; avoid concatenating conflicting defaults without explanation. Use headings and text that remain meaningful at the destination: adjust or remove relative links into this catalogue that would break after copying.

Copy only the selected guidance and create only directories that will be used by the requested work. Do not import this catalogue's Git metadata, change the target's remotes, overwrite unrelated files or generate empty layers for symmetry. Preserve licensing and attribution for redistributed guide content; do not replace the target project's license with this catalogue's license.

`ARCHITECTURE.md` is a project document, not a universally auto-loaded instruction file. Consult it during this task. If future discovery is requested, reference it from the project's existing instruction mechanism without replacing that mechanism or installing a global skill.

## 5. Continue the requested implementation

Implement the original task using the adopted decisions. Refactor only what is necessary to make that task coherent. Preserve behavior, public contracts, migrations, serialized assets and platform lifecycles as applicable.

For an adoption-only request, finish the architecture document and any useful structure within that scope. Do not invent product features or restructure an already suitable codebase just to demonstrate the pattern.

## 6. Verify and report

Review the resulting dependency direction and module boundary crossings. Run the relevant tests, build, lint or engine checks available in the target project. Inspect asset references, user-data compatibility or packaging when the change affects them. Documentation-only adoption needs document and link checks; it does not justify inventing runtime tests.

Report the selected guides and why, local architecture decisions, changed behavior and files, completed checks and any unavailable checks. Never present a successful documentation copy as validation of application behavior.

## Later updates

On a later invocation, inspect the current project and its local decisions again. If the user asks to refresh the reference, retrieve the new version, compare it with recorded provenance and merge relevant changes. Preserve local adaptations. This process does not provide background monitoring or automatic synchronization with the source repository.
