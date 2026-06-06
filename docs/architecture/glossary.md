# Glossary

| Term | Meaning |
|------|---------|
| **Bounded context** | A part of the system with its own model and language; changes inside it should not leak confusing terms to other parts. |
| **Strangler fig** | Migrate gradually: new behavior grows beside the old until the old can be retired. |
| **BOM (Bill of Materials)** | A Maven/Gradle artifact that pins compatible versions of related libraries. |
| **Hub module** | A library many other modules depend on; extract or change it last. |
| **Contract test** | Tests that verify an API between two components stays compatible. |
