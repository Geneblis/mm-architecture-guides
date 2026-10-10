# Adoption prompt

Send this request together with the architecture repository's link or the path to a local copy and the development task you want to complete.

```text
Use the architecture repository whose link or path I provided in this
message as a reference for the current project. Read its README.md and ADOPTION.md.

Analyze the technologies, existing structure, local instructions,
dependencies, and task requirements. Read Universal/ARCHITECTURE.md
and select environment guides suitable for the affected components.
Briefly explain the selection and adaptation before editing.

Incorporate the guidelines into an ARCHITECTURE.md in the current project.
If that file already exists, preserve local decisions and update only
what is necessary. Record the source, consulted revision when available,
and selected guides. Create only the folders and boundaries needed for
the task; use the examples as references and respect the structure
required by the framework or tool.

Combine Modular Monolith, Feature-Based Organization, and selective
Clean Architecture principles where appropriate. Preserve the existing
topology, contracts, and behavior. Do not impose layers, a new framework,
or a project-wide migration simply to adopt the guidelines.

After adoption, continue the implementation I requested within the
already authorized scope. Run the relevant available checks and report
decisions, changed files, and anything that could not be verified.

If my request is architecture adoption only, complete the documentation
and necessary structure without inventing a feature. If access to the
reference or project is unavailable, report that limitation without
claiming to have read them.
```
