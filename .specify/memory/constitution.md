<!--
Sync Impact Report
- Version change: template placeholders -> 1.0.0
- Modified principles:
  - Template Principle 1 -> 1. Simplicity First
  - Template Principle 2 -> 2. POC-Focused Development
  - Template Principle 3 -> 3. In-Memory Data Only
  - Template Principle 4 -> 4. Clean API Design
  - Template Principle 5 -> 5. Readable Code
  - Added principles: 6. Default Seed Data, 7. Minimal Dependencies
- Added sections:
  - Folder Structure Guidelines
  - Done Criteria
- Removed sections:
  - None
- Templates requiring updates:
  - ✅ updated: .specify/templates/plan-template.md
  - ✅ updated: .specify/templates/spec-template.md
  - ✅ updated: .specify/templates/tasks-template.md
  - ⚠ pending: .specify/templates/commands/*.md (directory not present in repository)
- Follow-up TODOs:
  - None
-->

# SpecDemoPOC Constitution

## Core Principles

### 1. Simplicity First
Implementation MUST remain minimal, direct, and easy to understand. Teams MUST reject
unnecessary abstraction layers and speculative architecture.
Rationale: simple designs reduce delivery risk and speed up learning in a POC.

### 2. POC-Focused Development
Work MUST prioritize learning speed over production hardening. Code MUST demonstrate
capability and expected flows, but it is not required to satisfy production non-functional
standards unless explicitly requested.
Rationale: this project exists to validate approach and feasibility quickly.

### 3. In-Memory Data Only
Data persistence for runtime scenarios MUST use EF Core InMemory provider. External
databases, migrations, and infrastructure dependencies MUST NOT be introduced.
Rationale: zero-environment setup keeps experimentation fast and reproducible.

### 4. Clean API Design
HTTP endpoints MUST follow REST conventions, use appropriate HTTP methods, and return
accurate status codes for success and failure paths.
Rationale: consistent API semantics make behavior testable and easy to consume.

### 5. Readable Code
Code MUST use clear, domain-appropriate naming and keep methods focused on a single
responsibility with limited scope.
Rationale: readability is required for rapid team iteration and review.

### 6. Default Seed Data
The application MUST start with sample product data available without manual actions.
Startup initialization MUST ensure deterministic seeded defaults.
Rationale: immediate usable state is necessary for quick demos and verification.

### 7. Minimal Dependencies
New third-party libraries MUST be justified by clear POC value that cannot be met with
built-in .NET capabilities. Built-in platform features SHOULD be preferred by default.
Rationale: reducing dependency surface lowers complexity and maintenance overhead.

## Folder Structure Guidelines

Repository implementation MUST organize code by responsibility:
- Controllers: API endpoints and request/response orchestration.
- Services: business logic and use-case behavior.
- Data: DbContext configuration and seeding logic.
- Models: domain entities and data contracts.

Any deviation from this structure MUST be justified in the feature plan under
Complexity Tracking.

## Done Criteria

A feature is complete only when all of the following are true:
- API endpoints are implemented and reachable.
- Data persists in memory for the application runtime session.
- Default seed data is loaded automatically.
- Basic validation is implemented for primary request paths.

## Governance

This constitution is the authoritative standard for project planning and implementation.
All plans, specs, tasks, and pull requests MUST include a constitution compliance check.

Amendment process:
- Changes MUST be proposed in writing with rationale and expected impact.
- Approval requires explicit agreement from project maintainers.
- Related templates and guidance files MUST be updated within the same change.

Versioning policy:
- MAJOR: backward-incompatible governance changes or principle removals/redefinitions.
- MINOR: new principles/sections or materially expanded guidance.
- PATCH: clarifications, wording improvements, and non-semantic edits.

Compliance review expectations:
- `/speckit.plan` MUST pass Constitution Check gates before design starts.
- `/speckit.tasks` MUST include tasks that satisfy Done Criteria and principle constraints.
- Reviews MUST block merges when violations are unresolved or unjustified.

**Version**: 1.0.0 | **Ratified**: 2026-04-01 | **Last Amended**: 2026-04-01
