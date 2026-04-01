# Implementation Plan: Baseline Product Management API

**Branch**: `[001-product-api-baseline]` | **Date**: 2026-04-01 | **Spec**: `/specs/001-product-api-baseline/spec.md`
**Input**: Feature specification from `/specs/001-product-api-baseline/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

Build a .NET 10 Web API baseline for Product Management with in-memory EF Core storage,
startup seed data, and CRUD REST endpoints. The solution emphasizes POC speed and
simplicity while enforcing clear validation, RFC 7807 error responses, and explicit
status code semantics (`200`/`201`/`204` and `404`/validation failures).

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: C# on .NET 10  
**Primary Dependencies**: ASP.NET Core Web API, Microsoft.EntityFrameworkCore, Microsoft.EntityFrameworkCore.InMemory  
**Storage**: EF Core InMemory provider with fixed database name (runtime-only persistence)  
**Testing**: Manual API verification via Swagger UI and HTTP client (Postman or equivalent)  
**Target Platform**: Local developer environment hosting ASP.NET Core Web API
**Project Type**: Web service (single backend API project)  
**Performance Goals**: Startup ready in under 30 seconds; responsive CRUD operations for demo-scale usage  
**Constraints**: No authentication/authorization, no external APIs, no persistent database, minimal dependencies  
**Scale/Scope**: Baseline POC for internal evaluators; single Product aggregate with CRUD and startup seed data

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- Simplicity First: design avoids unnecessary abstractions and speculative components.
- POC-Focused Development: scope targets capability demonstration, not production hardening.
- In-Memory Data Only: persistence uses EF Core InMemory with no external DB dependencies.
- Clean API Design: contracts follow REST methods and accurate HTTP status semantics.
- Readable Code: responsibilities are split into small, focused units with clear names.
- Default Seed Data: startup includes deterministic sample product data without manual setup.
- Minimal Dependencies: new libraries are justified only when built-in .NET features are insufficient.
- Folder Structure: implementation maps to Controllers, Services, Data, and Models.
- Done Criteria Coverage: plan includes endpoint readiness, in-memory persistence, seeding, and validation.

Pre-Phase 0 gate assessment:
- PASS: Plan keeps architecture minimal (controller + context + model; optional service only if needed).
- PASS: Scope remains POC-focused and excludes production hardening.
- PASS: Storage strictly in-memory with no external database dependencies.
- PASS: REST behavior and HTTP status semantics are explicitly defined.
- PASS: Readability constraints are reflected in structure and implementation approach.
- PASS: Startup seed data is mandatory and deterministic.
- PASS: Dependency footprint remains limited to required framework packages.
- PASS: Folder structure aligns to Controllers, Data, Models, and optional Services.

Post-Phase 1 design re-check:
- PASS: `research.md` confirms InMemory, startup seeding, and RFC 7807 decisions.
- PASS: `data-model.md` defines Product validation and lifecycle without over-engineering.
- PASS: `contracts/products.openapi.yaml` enforces REST/status/error semantics.
- PASS: `quickstart.md` verifies done criteria and no-manual-setup behavior.

## Project Structure

### Documentation (this feature)

```text
specs/001-product-api-baseline/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── products.openapi.yaml
└── tasks.md
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
SpecDemoPOC/
├── Program.cs
├── Controllers/
│   └── ProductsController.cs
├── Data/
│   ├── AppDbContext.cs
│   └── SeedData.cs
├── Models/
│   └── Product.cs
└── Services/ (optional)
```

**Structure Decision**: Use the existing single-project ASP.NET Core structure in `SpecDemoPOC/`
and add `Controllers`, `Data`, and `Models` folders with optional `Services` only if it improves
readability without adding unnecessary abstraction.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| None | N/A | N/A |
