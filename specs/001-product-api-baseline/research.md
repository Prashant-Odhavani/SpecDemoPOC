# Research: Baseline Product Management API

## Decision 1: API stack
- Decision: Use ASP.NET Core Web API on .NET 10 with attribute-routed controllers.
- Rationale: Matches current project scaffold, minimizes setup, and provides built-in model validation, routing, and Problem Details support.
- Alternatives considered:
  - Minimal APIs: lower ceremony but less aligned with the target folder conventions emphasizing Controllers.
  - gRPC: not suitable for the stated REST endpoint requirements.

## Decision 2: Data persistence approach
- Decision: Use Entity Framework Core with the InMemory provider and a fixed database name.
- Rationale: Satisfies constitution requirement for in-memory only persistence and enables fast startup with zero external dependencies.
- Alternatives considered:
  - SQLite in-memory mode: still adds relational behavior and setup complexity not required for POC baseline.
  - SQL Server/PostgreSQL: rejected due to external dependency and setup overhead.

## Decision 3: Seeding strategy
- Decision: Seed product data during application startup through a deterministic initializer that runs once per process start.
- Rationale: Guarantees at least 5 products available immediately and keeps behavior reproducible for demos and tests.
- Alternatives considered:
  - Lazy seeding on first request: adds request-path branching and makes startup state less explicit.
  - Manual seed endpoint: violates no-manual-setup success criterion.

## Decision 4: Validation and error contract
- Decision: Enforce validation via DataAnnotations and return RFC 7807 Problem Details for validation/not-found failures.
- Rationale: Clarified in spec decisions, standard machine-readable errors, and built-in framework support with minimal custom code.
- Alternatives considered:
  - Custom error DTO: possible but unnecessary for baseline and less interoperable.
  - Plain-text errors: not machine-friendly and harder to test.

## Decision 5: Update semantics
- Decision: Treat PUT as full resource update; all required fields must be present and valid.
- Rationale: Clarified in specification and keeps endpoint behavior deterministic.
- Alternatives considered:
  - Partial PUT semantics: ambiguous contract and harder client expectations.
  - PATCH endpoint in baseline: deferred to future feature expansion.

## Decision 6: Project structure
- Decision: Implement folders as Controllers, Data, Models, and Services (optional, only if needed for readability).
- Rationale: Directly matches constitution folder guidance and keeps code discoverable.
- Alternatives considered:
  - Flat structure in root: quicker initially but degrades readability as features expand.
  - Repository pattern layering: over-engineering for POC baseline.
