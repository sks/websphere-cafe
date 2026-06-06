# For developers (new to this repo)

## What this guidance PR is

Architecture notes from an automated scan of this repository. Use them to understand how the codebase is grouped before any split work.

## Your next 3 steps

1. Read the [architecture README](README.md) (5 minutes).
2. Run baseline tests: `mvn test`
3. Explore the **hub module** first: `.`

## Do not break

- Do not change public APIs in the hub module without coordinating all dependents.
- Add or extend unit tests before moving code across module boundaries.

<!-- LLM enrichment may extend sections below -->
