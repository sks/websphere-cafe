# Migration phases (library / multi-module repo)

## Phase 0 — Tests and toolchain

Ensure Java/Go/Node toolchain matches repo requirements; `./gradlew test` or equivalent green.

## Phase 1 — Stabilize shared kernel

Lock APIs for the hub module; publish SNAPSHOT or document internal-only status.

## Phase 2 — Extract leaf modules

Publish independent artifacts for modules with low inbound coupling (see `coupling-matrix.json` extraction_order).

## Phase 3 — Framework and integration modules

Extract adapters (Spring, Reactor, etc.) after core pattern libraries have stable coordinates.

## Phase 4 — BOM and consumer alignment

Update BOM and downstream consumer version pins; run compatibility tests.

Suggested extraction order (from coupling scan):
- .
