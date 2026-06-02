# Modernization Plan: WebSphere Cafe

## Executive Summary
This document outlines the strategy for modernizing the WebSphere Cafe application from a traditional WebSphere Application Server (tWAS) environment to a cloud-native, microservices-based architecture.

## Current State Analysis
- **Platform**: IBM WebSphere Application Server (Traditional).
- **Runtime**: Java EE 7 (Java 1.8).
- **Architecture**: Monolithic EAR containing WAR and EJB modules.
- **Key Components**: JSF (Web UI), JAX-RS (REST API), JPA (Data Access), JNDI (Data Sources).
- **Infrastructure**: On-premises or VM-based hosting, manual scaling, licensing costs associated with IBM WebSphere.

## Target Architecture
- **Runtime**: Open Liberty or Quarkus (Jakarta EE / MicroProfile).
- **Deployment**: Containerized (Docker/OCI) on Kubernetes (AKS/EKS/GKE).
- **Communication**: REST/gRPC for service-to-service.
- **Persistence**: Managed Cloud Databases (Azure SQL / PostgreSQL).

## CCE (Cloud Cost Entitlements) Analysis
- **Current**: IBM WebSphere traditional licenses are expensive and tied to PVU/VPC metrics.
- **Modernized**: Moving to Open Liberty (Open Source or IBM Liberty) significantly reduces licensing overhead. Transitioning to Pay-As-You-Go cloud resources (AKS/App Service) optimizes cost based on actual usage.

## Migration Strategy: Strangler Fig Pattern
1. **Containerize**: Move the monolith to Open Liberty in a container.
2. **Expose**: Refactor JNDI to environment-based configuration.
3. **Extract**: Carve out the REST API as a separate microservice.
4. **Decouple**: Move the JSF UI to a modern SPA (React/Vue) or keep it as a legacy frontend communicating with microservices.

## Phases
### Phase 1: Containerization
- Use `icr.io/appcafe/open-liberty` as the base image.
- Configure `server.xml` to support Java EE 7 features.
### Phase 2: Microservice Extraction
- Split the `CafeResource` into a standalone Spring Boot or Quarkus service.
### Phase 3: Cloud-Native Deployment
- Deploy to Kubernetes with Helm charts. Implement Readiness/Liveness probes.
### Phase 4: Persistence Modernization
- Transition from JTA/JNDI to Spring Data JPA or Micronaut Data.

## Risk Register
- **JNDI Dependencies**: High. Action: Externalize config via MicroProfile Config.
- **JSF Lifecycle**: Complex. Action: Phased UI replacement.

## Test Strategy
- Unit tests for new microservices.
- Contract testing (Pact) between UI and API.
- E2E tests using Playwright.
