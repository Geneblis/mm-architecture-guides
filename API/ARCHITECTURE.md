# ARCHITECTURE.md — Backend APIs & Services

> **Default:** Feature-oriented Modular Monolith; keep transport, application rules, and persistence boundaries clear **without mandatory layer stacks**.

## Principles

1. Inspect existing endpoints, domain concepts, database schema, authentication, external dependencies, and deployment constraints before changing architecture.
2. Group each capability's endpoint/handler, rules, validation, and data access near its feature when sensible.
3. Keep HTTP/gRPC transport concerns at the edge; avoid embedding substantial business rules in controllers or routing code.
4. Features communicate through explicit operations or contracts—not each other's database tables, private repositories, or implementation classes.
5. Put cross-cutting authentication, authorization, logging, and error translation in established middleware/infrastructure; enforce access control at every relevant boundary.
6. Validate untrusted inputs at ingress; maintain data invariants and transaction boundaries where changes are committed.
7. Use direct calls for synchronous business collaboration; queues/events only when decoupling, reliability, or async processing **actually** requires them.
8. Add repositories/interfaces only when they hide meaningful persistence complexity or enable real substitutions; direct ORM/query access can be fine in a simple feature or persistence adapter. Rules declared independent of persistence must not import the ORM, queries or database-specific types; connect external effects through narrow rule-owned contracts or callbacks.
9. Preserve API compatibility, database migrations, error semantics, and operational observability during refactors.
10. Handle retries, idempotency, caching, rate limits, and performance according to actual endpoint requirements—not as universal boilerplate.

## Suggested layout (illustrative)

```text
src/
  app/                    # entry point, middleware, dependency wiring
  features/
    users/                # endpoints + logic + persistence
    billing/
    orders/
  infrastructure/         # external adapters shared across features
  shared/                 # truly cross-cutting primitives
```

## Agent workflow

- Trace endpoint -> authorization -> feature rule -> storage/external effect.
- Limit changes to the owning feature plus necessary public contracts and migrations.
- Validate tests, API schema, authentication, transactions, and backward compatibility.
- Avoid introducing CQRS, event sourcing, microservices, or generic repository layers without a concrete need.

**Boundary test:** Changing order rules should not require reaching into billing's private database implementation.
