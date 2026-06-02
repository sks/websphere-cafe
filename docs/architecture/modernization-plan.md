# WebSphere Cafe — Modernization and Upgrade Plan

## Executive Summary
websphere-cafe is a Java EE 7 CRUD application currently deployed on IBM WebSphere Application Server. It uses EAR/WAR packaging, JAX-RS REST endpoints, JSF frontend, JPA 2.1 with OpenJPA, CDI, and WebSphere-specific descriptors (ibm-web-ext.xml). The application has zero unit tests (test_confidence_score=0.0), making any migration high-risk without a tests-first phase.

Target state: migrate to a cloud-native runtime (Jakarta EE 10 on Open Liberty, Spring Boot 3, or Quarkus), containerize, and deploy to Azure (AKS or App Service) using Managed Identity for Azure SQL authentication. CCE scan found 0 cloud entitlements in the main app — no AWS/GCP/Azure SDK calls to migrate.

## Current Architecture
| Component | Details |
|---|---|
| Language | Java 8 |
| Build | Maven multi-module |
| Packaging | EAR (websphere-cafe-application) + WAR (websphere-cafe-web) |
| REST | JAX-RS @Path(coffees) — GET, POST, DELETE |
| Persistence | JPA 2.1, OpenJPA, JNDI datasource jdbc/WebSphereCafeDB |
| Frontend | JSF + *.xhtml, i18n (EN + ES) |
| DI | CDI 1.1, bean-discovery-mode=all |
| WAS-specific | ibm-web-ext.xml, EAR packaging, JTA datasource |
| Tests | 0 unit tests, 0 integration tests |
| Cloud APIs | 0 (CCE scan: 57 files, 0 entitlements) |

## Modernization Paths
### Path A: Jakarta EE 10 + Open Liberty (Recommended)
- Migrate javax.* → jakarta.* namespace
- Replace OpenJPA with Hibernate 6 or EclipseLink 4
- Remove ibm-web-ext.xml and EAR packaging
- Keep JAX-RS, CDI, JPA, JSF (Jakarta Faces 4.0)
- Containerize with Docker, deploy to AKS or Azure App Service
- Effort: Medium | Risk: Low-Medium | Azure fit: High

### Path B: Spring Boot 3 + Spring Data JPA
- Replace JAX-RS with Spring MVC, CDI with Spring DI, JPA with Spring Data
- Replace JSF with Thymeleaf or React SPA
- Drop EAR, embed Tomcat, deploy as fat JAR
- Effort: High | Risk: Medium | Azure fit: High

### Path C: Quarkus
- Compile-time CDI, MicroProfile JAX-RS, Hibernate ORM Panache
- Native image option for fast startup
- Drop EAR/WAR, deploy as container
- Effort: Medium-High | Risk: Medium | Azure fit: High

## WebSphere Removal Checklist
- [ ] Remove ibm-web-ext.xml
- [ ] Remove EAR packaging (websphere-cafe-application module)
- [ ] Replace JNDI datasource (jdbc/WebSphereCafeDB) with env-var config
- [ ] Replace OpenJPA with Hibernate 6 or EclipseLink 4
- [ ] Migrate javax.* → jakarta.* (all 4 Java files affected)
- [ ] Replace schema-generation=create with Flyway or Liquibase migrations

## Database and Persistence Modernization
- Replace JNDI datasource with environment-variable-driven connection
- Replace OpenJPA with Hibernate 6 / EclipseLink 4
- Add Flyway or Liquibase for schema migrations (replace schema-generation=create)
- Adopt Azure Entra ID authentication (ActiveDirectoryDefault JDBC) for Azure SQL — pattern already proven in util/azure-sql-query
- Use HikariCP (Spring Boot) or Agroal (Quarkus) for connection pooling

## Cloud Entitlements and IAM
- CCE scan: 0 entitleme
