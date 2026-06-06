# AGENTS.md

Agent instructions for this repository. Generated during Guild monorepo split analysis
(script pack 20260604.7). Format: [agents.md](https://agents.md/).

## Project overview

This is the basic Java EE application used throughout the WebSphere on Azure demos.
It is a simple CRUD application. It uses Maven and Java EE 7 (JAX-RS, EJB, CDI, JPA, JSF, Bean Validation).

- **Languages detected:** java
- **Modules / packages scanned:** 1
- **Test confidence score:** 0 (0–1, from unit-test inventory)
- **Test frameworks:** unknown

## Setup commands

- Install/build (skip tests): `mvn -q -DskipTests package`

## Testing instructions

Run the language-appropriate suite before opening PRs. Prefer the same commands CI uses.

- Java: `mvn test`

- Fix failing tests before merge; do not disable tests to land split/refactor work.
- Packages without unit tests (high coupling cut risk): see `packages_without_tests` in `docs/architecture/coupling-matrix.json`.

## Code style and conventions

- See `CONTRIBUTING.md` for contributor guidelines

## Monorepo / split context

This repo was analyzed for service extraction. Architecture artifacts live under `docs/architecture/`:

- `service-catalog.yaml` — proposed target services
- `migration-phases.md` — strangler-fig ordering
- `bounded-context-map.mermaid` — DDD context map
- `coupling-matrix.json` — scan output including `test_inventory`

When extracting a service, keep **unit tests co-located** with the code you move and add contract tests at new HTTP/gRPC boundaries.

## PR instructions

- Open PRs against the default branch; use feature branches (`guild/split-*` for Guild-generated work).
- Include test evidence for touched packages (CI log snippet or local command output).
- Do not push directly to the default branch.

