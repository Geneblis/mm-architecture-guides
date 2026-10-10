# Architecture Guides

Architecture guides for coding agents: analyze the project, adapt suitable guidelines, and continue implementation.

This repository combines **Modular Monolith**, **Feature-Based Organization**, and **selective Clean Architecture principles**. Share its link with an agent during a development task; the agent reads the guides and incorporates an appropriate architecture into the current project. The same process works with a local copy of this folder.

No skill, plugin, framework, or global configuration is required. These files are reference documents with example layouts, rather than executable starter projects or code generators.

## How to use

Share this repository's link together with the task you want to complete. For example:

```text
Use the architecture repository whose link I provided in this message.
Analyze my project, select suitable guides, and incorporate an adapted
version into ARCHITECTURE.md. Create only the structure needed for the task,
respect existing conventions, and continue the requested implementation.
```

For a more detailed request, use the [reusable prompt](PROMPT.md). The [adoption workflow](ADOPTION.md) explains how to retrieve, select, incorporate, and verify the guidelines.

The agent needs access to the remote repository or a local copy and permission to edit the target project. Sharing a link alone does not grant access to your local project files.

## What the agent does

1. Reads this README and the adoption workflow.
2. Inspects the target project's technologies, structure, local instructions, affected features, and execution constraints.
3. Reads the Universal guide and relevant environment guides, explaining its selection.
4. Creates or updates an adapted `ARCHITECTURE.md` with project decisions and guide provenance.
5. Creates folders and changes code only when they support the requested task, then continues implementation and runs available checks.

If you request architecture adoption only, the result is documentation and any necessary structure. The agent does not invent a feature to implement.

## Available guides

| Guide | When to use it |
| --- | --- |
| [Universal](Universal/ARCHITECTURE.md) | Shared principles and environments without a dedicated guide, including libraries, mods, and projects whose structure is imposed by their tools. |
| [API](API/ARCHITECTURE.md) | Backend services, endpoints, persistence, and integrations. |
| [Web](Web/ARCHITECTURE.md) | Websites, web applications, routes, components, and browser/server boundaries. |
| [Desktop](Desktop/ARCHITECTURE.md) | Desktop applications, operating-system integration, and UI lifecycle. |
| [Mobile](Mobile/ARCHITECTURE.md) | Mobile applications, navigation, lifecycle, and device storage. |
| [CLI](CLI/ARCHITECTURE.md) | Command-line tools, automation, arguments, and external effects. |
| [Unity](Unity/ARCHITECTURE.md) | Unity projects with scripts, scenes, prefabs, and assets. |
| [Unreal](Unreal/ARCHITECTURE.md) | Unreal projects with C++, Blueprints, Actors, and assets. |

Projects spanning multiple environments can use several guides. A web application with its own backend can combine **Web + API**, applied to the respective components. A Unity client with a backend can combine **Unity + API**, preserving each environment's lifecycle. A remote backend does not make the entire system a single monolith.

## How the three principles fit together

They describe different architectural dimensions rather than three mandatory layers:

| Principle | What it defines | How to apply it |
| --- | --- | --- |
| Modular Monolith | Boundaries and collaboration between modules within an application deployed as one unit. | Each module owns its data and internals and exposes clear operations. |
| Feature-Based Organization | Organization by feature or capability. | Keep files belonging to the same feature close together, respecting the framework. |
| Clean Architecture | Dependency direction and separation between rules and technical details. | Where rules are isolated, UI, storage, and integrations depend on those rules; the rules do not import external details. |

A feature can be a module in a small project. In larger projects, a business module may contain several features. Creating a folder does not guarantee isolation: contracts, dependencies, and data ownership establish the boundaries.

**This catalogue applies Clean Architecture selectively.** A simple feature may use an ORM directly; a rule that must remain independent of the database should be separated from that access. Direct ORM access inside a domain described as isolated would violate that separation. There is no requirement to create `domain/`, `application/`, and `infrastructure/` folders in every feature.

A modular monolith is a preference for applications where it fits. Distributed systems, extensions, libraries, and mods retain their topology and platform-required structures. Apply the compatible principles without forcing a conversion.

## What “clone the architecture” means

It means incorporating the selected guidelines and adapting their organization to the project. The agent may clone this repository into a temporary folder for reading or retrieve only the required documents.

In the target project, it copies or composes relevant guidance into `ARCHITECTURE.md` and creates the structure that will actually be used. Directory examples are illustrative: the agent should not copy every environment, import this catalogue's `.git` directory, or replace the project's remotes.

An `ARCHITECTURE.md` is documentation. Whether it is read automatically depends on the agent; ask the agent to consult it in future tasks or reference it from the local instructions already used by the project.

## Changes during development

- **The project changed:** when these guidelines are used again, the agent inspects current files and updates the relevant local decisions.
- **The guides changed:** request a fresh repository lookup and comparison with the adopted version. Local copies do not synchronize automatically.
- **The existing architecture already supports the task:** preserve it and record only useful criteria. Adoption may not require moving code.

Record the source URL or path, the consulted revision when available, and the selected guides in the local document. This allows version comparisons without losing project-specific decisions.

## Repository layout

```text
README.md                Overview, guide selection, and limitations
PROMPT.md                Reusable request for the agent
ADOPTION.md              Adoption workflow for the target project
REVIEW.md                Consistency review of all eight guides
Universal/ARCHITECTURE.md Shared principles
API/ARCHITECTURE.md       Backend and services
Web/ARCHITECTURE.md       Web applications
Desktop/ARCHITECTURE.md   Desktop applications
Mobile/ARCHITECTURE.md    Mobile applications
CLI/ARCHITECTURE.md       Command-line tools
Unity/ARCHITECTURE.md     Unity
Unreal/ARCHITECTURE.md    Unreal
LICENSE                  Apache-2.0
```

Documentation is written in English for reuse across projects and agents. The [consistency review](REVIEW.md) records the corrections and scenarios examined.

## License

Distributed under the [Apache License 2.0](LICENSE). When redistributing catalogue files, preserve the license and applicable attribution.
