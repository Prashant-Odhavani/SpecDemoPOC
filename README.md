# SpecDemoPOC

A .NET 10 Web API proof of concept for product management using EF Core InMemory storage.

## What this POC includes

- Product CRUD API under `/api/products`
- In-memory persistence (no external database)
- Deterministic seed data loaded at startup
- Problem Details error responses
- OpenAPI support in development
- Speckit-driven spec to implementation workflow in `specs/`

## Tech stack

- .NET SDK 10
- ASP.NET Core Web API
- EF Core InMemory

## Project structure

- `SpecDemoPOC/` - API project
- `specs/001-product-api-baseline/` - generated feature artifacts (spec, plan, tasks, contracts, quickstart)
- `.specify/` - Speckit templates, memory, and automation scripts
- `.github/agents/` - Speckit agent command definitions

## Run the API

1. Open a terminal at repo root.
2. Start the API:

```powershell
dotnet run --project SpecDemoPOC/SpecDemoPOC.csproj
```

3. Open the OpenAPI/Swagger endpoint shown in console output.
4. Optionally run request samples from `SpecDemoPOC/SpecDemoPOC.http`.

## Speckit end-to-end workflow (installation to implementation)

This repository is already Speckit-enabled (`.specify/` and `.github/agents/` exist). Use this process for all new features.

### 1) Installation and prerequisites

1. Install VS Code.
2. Install Git.
3. Install .NET SDK 10.x.
4. Install and sign in to GitHub Copilot + Copilot Chat in VS Code.
5. Open this repository in VS Code.
6. Verify Speckit scaffolding exists:

```powershell
Get-ChildItem .specify
Get-ChildItem .github/agents/speckit*.agent.md
```

If these folders are missing in a new repo, bootstrap Speckit first using your team template/process, then continue.

### 2) Create a feature spec

In Copilot Chat, run:

```text
/speckit.specify Build product search with name and category filters
```

What this does:
- Creates a feature branch like `002-product-search`
- Creates feature folder `specs/002-product-search/`
- Generates `spec.md` and a quality checklist

### 3) Clarify open requirements (optional but recommended)

If `spec.md` has clarification markers, run:

```text
/speckit.clarify
```

Answer the questions, then confirm `spec.md` is fully resolved.

### 4) Generate implementation plan

Run:

```text
/speckit.plan
```

This generates/updates:
- `plan.md`
- `research.md`
- `data-model.md`
- `quickstart.md`
- `contracts/` artifacts (such as OpenAPI)

### 5) Generate executable tasks

Run:

```text
/speckit.tasks
```

This creates `tasks.md` with:
- ordered phases
- user story mapping
- parallelizable tasks markers
- file-level implementation hints

### 6) Analyze consistency before coding

Run:

```text
/speckit.analyze
```

Review and resolve any critical or high issues before implementation.

### 7) Implement tasks

Run:

```text
/speckit.implement
```

Speckit executes tasks from `tasks.md` phase by phase and marks completed items.

### 8) Validate and verify

1. Build and run:

```powershell
dotnet build SpecDemoPOC.sln
dotnet run --project SpecDemoPOC/SpecDemoPOC.csproj
```

2. Execute quickstart/manual checks from:
- `specs/<feature>/quickstart.md`
- `SpecDemoPOC/SpecDemoPOC.http`

3. Confirm:
- endpoints behave as specified
- Problem Details responses are correct
- seed data and in-memory behavior match plan/spec

### 9) Finalize

1. Review changed files.
2. Commit with a clear message.
3. Push branch and open PR.
4. Include links to `spec.md`, `plan.md`, and `tasks.md` in PR description.

## Existing baseline feature in this repo

Current implemented feature artifacts are in:

- `specs/001-product-api-baseline/spec.md`
- `specs/001-product-api-baseline/plan.md`
- `specs/001-product-api-baseline/tasks.md`
- `specs/001-product-api-baseline/quickstart.md`
- `specs/001-product-api-baseline/contracts/products.openapi.yaml`

## Notes

- Data is intentionally non-persistent across restarts (InMemory provider).
- This is a POC and intentionally optimized for simplicity and fast iteration.
