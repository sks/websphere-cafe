# WebSphere Cafe Modernization Plan

## Executive Summary
websphere-cafe is a Java EE 7 CRUD application on IBM WebSphere. Target: migrate to Jakarta EE 10 on Open Liberty or Spring Boot 3, containerize, deploy to Azure. Zero unit tests exist (test_confidence_score=0.0) — tests-first phase is mandatory. CCE scan: 0 cloud entitlements in main app.

## Current Architecture
- Language: Java 8, Maven multi-module
- Modules: websphere-cafe-web (WAR), websphere-cafe-application (EAR), util/azure-sql-query (standalone)
- REST: JAX-RS at /rest/coffees (GET, POST, DELETE)
- Persistence: JPA 2.1 + OpenJPA, JNDI datasource jdbc/WebSphereCafeDB
- Frontend: JSF + xhtml, i18n EN+ES
- DI: CDI 1.1
- WebSphere-specific: ibm-web-ext.xml, EAR packaging, JTA datasource
- Tests: 0 unit tests, 0 integration tests
- Cloud APIs: 0 (CCE scan: 57 files, 0 entitlements)

## Modernization Paths

### Path A: Jakarta EE 10 + Open Liberty (Recommended)
Migrate javax to jakarta namespace, replace OpenJPA with Hibernate 6, remove ibm-web-ext.xml and EAR, keep JAX-RS+CDI+JPA+JSF, containerize, deploy to AKS or App Service. Effort: Medium, Risk: Low-Medium, Azure fit: High.

### Path B: Spring Boot 3
Replace JAX-RS with Spring MVC, CDI with Spring DI, JPA with Spring Data, JSF with Thymeleaf or React. Drop EAR, embed Tomcat. Effort: High, Risk: Medium, Azure fit: High.

### Path C: Quarkus
Compile-time CDI, MicroProfile JAX-RS, Hibernate ORM Panache, native image. Effort: Medium-High, Risk: Medium, Azure fit: High.

## WebSphere Removal Checklist
- Remove ibm-web-ext.xml
- Remove EAR packaging
- Replace JNDI datasource with env-var config
- Replace OpenJPA with Hibernate 6
- Migrate javax to jakarta namespace
- Replace schema-generation=create with Flyway or Liquibase

## Database Modernization
- Replace JNDI datasource with environment-variable connection string
- Replace OpenJPA with Hibernate 6
- Add Flyway for schema migrations
- Adopt Azure Entra ID auth (ActiveDirectoryDefault JDBC) for Azure SQL
- Use HikariCP or Agroal for connection pooling

## Cloud Entitlements and IAM
- CCE scan: 0 entitlements in main app
- util/azure-sql-query uses Entra ID auth - adopt for main app
- Use Azure Managed Identity + Entra ID auth (no passwords in config)
- AKS: Workload Identity bound to pod service account
- App Service: system-assigned managed identity

## Unit Test Gap
- MANDATORY before migration
- 0 unit tests, test_confidence_score=0.0, HIGH risk
- Add JUnit 5 + Mockito + maven-surefire-plugin 3.x
- Unit test CafeRepository, CafeResource, Coffee entity
- Integration test with Testcontainers (SQL Server or H2)
- Target: 70%+ unit test coverage before any split

## Migration Roadmap
- Phase 1: Test Baseline (Add unit tests)
- Phase 2: Jakarta EE 10 Migration (javax -> jakarta)
- Phase 3: Open Liberty Adoption (Remove WebSphere specific config)
- Phase 4: Containerization (Dockerfile + Azure CI/CD)
