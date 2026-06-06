# For architects (boundaries and risk)

## Evidence-first review

- **Dependency graph:** `coupling-matrix.json` (machine-generated from build files).
- **Hub module:** `.` — highest inbound coupling; treat as shared kernel.
- **Cloud / outbound coupling:** see `cce_summary` in scan notes and optional `cce-*.json` artifacts.

## Anti-patterns to avoid

- Declaring network microservices for pure library modules (JAR/npm packages).
- Cutting through the hub without a versioned client SDK or BOM strategy.

## Your next 3 steps

1. Validate clusters in `service-catalog.yaml` against `coupling-matrix.json`.
2. Confirm `repo_archetype` matches how you ship software (library vs runnable services).
3. Record ADR references in PR comments if you disagree with a proposed group.

<!-- LLM enrichment may extend sections below -->
