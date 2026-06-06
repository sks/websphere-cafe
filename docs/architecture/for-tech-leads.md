# For tech leads (planning delivery)

## Migration stance

Follow `migration-phases.md` in order. Each phase should end with green CI on the paths you touched.

## Gates before extraction

- Baseline test command green on the default branch (or documented environment constraint).
- No extraction through modules listed in `packages_without_tests` without a tests-first sub-phase.

## Your next 3 steps

1. Agree on `repo_archetype` and service/module groups in `service-catalog.yaml`.
2. Assign an owner per group for Phase 0 test remediation (if needed).
3. Schedule contract tests at any new publish or HTTP boundary.

<!-- LLM enrichment may extend sections below -->
