# ARCHITECTURE.md — CLI Tools & Automation

> **Default:** Small feature-oriented monolith; keep command behavior clear and platform interactions explicit.

## Principles

1. Inspect commands, flags, configuration, environment assumptions, filesystem effects, and current output contracts before changes.
2. Group command-specific parsing, workflow, and helpers together; do not force every command into multiple layers.
3. Separate parsing/validation from operations that modify files, call networks, or launch processes when that improves safety and testing.
4. Expose reusable operations as small functions; keep the CLI entry point focused on wiring and exit behavior.
5. Avoid hidden global state, side effects at import time, and commands that unexpectedly modify the working directory.
6. Distinguish structured stdout from diagnostic stderr; use meaningful exit codes and actionable error messages.
7. Treat file paths, input arguments, environment variables, and subprocess arguments as untrusted; handle quoting and platform differences safely.
8. Prefer direct function calls over plugin systems, event buses, dependency containers, or extensive interfaces.
9. Add shared helpers only when multiple commands truly need them; prefer explicit dependencies.
10. Maintain backward compatibility for flags, output formats, scripts, and configuration where relevant; optimize only after measurement.

## Suggested layout (illustrative)

```text
src/
  main.*                  # CLI entry point, arguments, exit status
  commands/
    import/               # command-specific workflow
    export/
    validate/
  shared/                 # common parsing/IO helpers when needed
```

## Agent workflow

- Identify the command and every external side effect before editing.
- Keep the patch localized, favor readable error paths, and preserve existing flags/output.
- Verify commands with representative valid/invalid inputs and dry-run behavior when supported.
- Do not introduce a framework for a handful of functions.

**Boundary test:** Updating `import` should not change how `export` behaves unless their shared contract intentionally changes.
