# Tasks: Baseline Product Management API

**Input**: Design documents from `/specs/001-product-api-baseline/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**Tests**: Automated tests are not explicitly requested in the feature spec; validation is performed through manual acceptance checks in quickstart.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Prepare the existing .NET Web API project for baseline implementation.

- [X] T001 Remove sample weather endpoint mapping in SpecDemoPOC/Program.cs
- [X] T002 Remove sample controller file SpecDemoPOC/Controllers/WeatherForecastController.cs
- [X] T003 Remove sample model file SpecDemoPOC/WeatherForecast.cs
- [X] T004 Add EF Core package references in SpecDemoPOC/SpecDemoPOC.csproj
- [X] T005 [P] Replace sample request collection in SpecDemoPOC/SpecDemoPOC.http

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Implement core data and API infrastructure required before user story implementation.

**CRITICAL**: No user story work starts until this phase is complete.

- [X] T006 Create Product entity with validation attributes in SpecDemoPOC/Models/Product.cs
- [X] T007 Create application DbContext with DbSet<Product> in SpecDemoPOC/Data/AppDbContext.cs
- [X] T008 Create seed initializer scaffold in SpecDemoPOC/Data/SeedData.cs
- [X] T009 Configure fixed-name InMemory DbContext registration in SpecDemoPOC/Program.cs
- [X] T010 Enable consistent Problem Details responses in SpecDemoPOC/Program.cs
- [X] T011 Add startup seed invocation pipeline in SpecDemoPOC/Program.cs
- [X] T012 Create baseline products controller skeleton in SpecDemoPOC/Controllers/ProductsController.cs

**Checkpoint**: Foundation ready - user story implementation can proceed.

---

## Phase 3: User Story 1 - View Product Catalog (Priority: P1) 🎯 MVP

**Goal**: Allow clients to list products and get a product by id with proper not-found behavior.

**Independent Test**: Call `GET /api/products` and `GET /api/products/{id}` for existing and non-existing ids, verifying `200` and `404` Problem Details outcomes.

### Implementation for User Story 1

- [X] T013 [US1] Implement GET collection endpoint in SpecDemoPOC/Controllers/ProductsController.cs
- [X] T014 [US1] Implement GET by-id endpoint with 404 handling in SpecDemoPOC/Controllers/ProductsController.cs
- [X] T015 [P] [US1] Align GET endpoint response contract details in specs/001-product-api-baseline/contracts/products.openapi.yaml

**Checkpoint**: User Story 1 is independently functional and demoable.

---

## Phase 4: User Story 2 - Manage Product Records (Priority: P2)

**Goal**: Provide create, full update, and delete operations with required validation and status semantics.

**Independent Test**: Create product (valid and invalid), full update product (valid/missing required fields/non-existing id), and delete product (existing/non-existing id), verifying `201`, `200`, `204`, `400`, and `404` behaviors.

### Implementation for User Story 2

- [X] T016 [P] [US2] Create upsert request model with validation rules in SpecDemoPOC/Models/ProductUpsertRequest.cs
- [X] T017 [US2] Implement POST endpoint with server-generated id and client-id rejection in SpecDemoPOC/Controllers/ProductsController.cs
- [X] T018 [US2] Implement full PUT endpoint requiring all mandatory fields in SpecDemoPOC/Controllers/ProductsController.cs
- [X] T019 [US2] Implement DELETE endpoint with 204/404 behavior in SpecDemoPOC/Controllers/ProductsController.cs
- [X] T020 [US2] Align controller error payloads with RFC 7807 responses in SpecDemoPOC/Controllers/ProductsController.cs

**Checkpoint**: User Story 2 is independently functional without requiring additional story work.

---

## Phase 5: User Story 3 - Start With Usable Baseline Data (Priority: P3)

**Goal**: Ensure startup always provides realistic seeded products with no manual setup.

**Independent Test**: Start API from clean run and verify first `GET /api/products` returns at least five realistic products with unique ids.

### Implementation for User Story 3

- [X] T021 [US3] Populate deterministic default product dataset in SpecDemoPOC/Data/SeedData.cs
- [X] T022 [US3] Add idempotent seeding guard to prevent duplicate seed inserts in SpecDemoPOC/Data/SeedData.cs
- [X] T023 [US3] Ensure seeding executes before request handling on startup in SpecDemoPOC/Program.cs

**Checkpoint**: User Story 3 startup-readiness behavior is independently verifiable.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final cleanup and cross-story verification.

- [X] T024 [P] Update quickstart verification steps in specs/001-product-api-baseline/quickstart.md
- [X] T025 [P] Synchronize API contract details in specs/001-product-api-baseline/contracts/products.openapi.yaml
- [ ] T026 Run manual end-to-end API validation scenarios in SpecDemoPOC/SpecDemoPOC.http
- [X] T027 Remove or adjust remaining baseline noise comments in SpecDemoPOC/Program.cs

---

## Dependencies & Execution Order

### Phase Dependencies

- Setup (Phase 1): Starts immediately.
- Foundational (Phase 2): Depends on Setup completion; blocks all user stories.
- User Stories (Phases 3-5): Start after Foundational completion; execute in priority order for incremental delivery.
- Polish (Phase 6): Starts after selected user stories are complete.

### User Story Dependencies

- US1 (P1): Depends only on foundational phase.
- US2 (P2): Depends on foundational phase and reuses controller/data model from US1.
- US3 (P3): Depends on foundational phase and seed scaffold; independent from US2 business behavior.

### Suggested Completion Order

- US1 -> US2 -> US3

---

## Parallel Opportunities

- Setup parallelism: T005 can run in parallel with T001-T004.
- Foundational parallelism: T006, T007, and T008 can run in parallel before Program wiring tasks.
- US2 parallelism: T016 can run in parallel with early controller work before endpoint wiring.
- Polish parallelism: T024 and T025 can run in parallel.

### Parallel Example: User Story 1

- Execute T013 in SpecDemoPOC/Controllers/ProductsController.cs and T015 in specs/001-product-api-baseline/contracts/products.openapi.yaml in parallel.

### Parallel Example: User Story 2

- Execute T016 in SpecDemoPOC/Models/ProductUpsertRequest.cs while endpoint flow is prepared in SpecDemoPOC/Controllers/ProductsController.cs.

### Parallel Example: User Story 3

- Execute T021 in SpecDemoPOC/Data/SeedData.cs in parallel with startup pipeline verification prep for T023 in SpecDemoPOC/Program.cs.

---

## Implementation Strategy

### MVP First (US1)

1. Complete Phase 1 and Phase 2.
2. Deliver Phase 3 (US1) and validate independently.
3. Demo baseline read behavior with seeded data availability.

### Incremental Delivery

1. Add US2 for complete CRUD behavior and validation/error semantics.
2. Add US3 to guarantee startup-ready seeded baseline dataset.
3. Finish with polish and contract/quickstart synchronization.

### Team Strategy

1. Developer A: Program/Data foundational wiring.
2. Developer B: ProductsController endpoint implementation.
3. Developer C: Spec artifacts updates (quickstart/contracts) and manual validation execution.

---

## Notes

- All tasks use the required checklist format: `- [ ] T### [P] [US#] Description with file path`.
- `[P]` is only used where work can proceed on different files without waiting for unfinished dependencies.
- User story labels are applied only in user story phases.
- Keep implementation aligned with constitution constraints: simplicity, in-memory-only data, default seed data, and minimal dependencies.
