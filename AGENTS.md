# Developer & Agent Onboarding Guide

## Setup Commands
```bash
mvn clean package
# Run locally with Liberty
mvn liberty:run
```

## Architecture Conventions
- All new services must follow the **Sidecar Pattern** for observability.
- Use **OpenTelemetry** for tracing.
- Prefer **C4 Model** for diagramming.

## Split Guidance
- Do not split entities that share a database transaction.
- Use **Transactional Outbox** for cross-service consistency.
