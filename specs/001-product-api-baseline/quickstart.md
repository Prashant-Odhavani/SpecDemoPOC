# Quickstart: Baseline Product Management API

## Prerequisites
- .NET SDK 10.x installed.

## Run the API
1. From repository root, start the API project:
   - `dotnet run --project SpecDemoPOC/SpecDemoPOC.csproj`
2. Open Swagger UI from the launch URL shown in console output.
3. Optionally execute [SpecDemoPOC/SpecDemoPOC.http](SpecDemoPOC/SpecDemoPOC.http) requests in order for a quick manual verification pass.

## Validate Baseline Behavior

### 1) Verify seeded data
1. Call `GET /api/products`.
2. Confirm at least 5 products are returned.

### 2) Verify get by id
1. Use an existing product Id from list response.
2. Call `GET /api/products/{id}` and confirm `200`.
3. Call with a non-existent Id and confirm `404` Problem Details.

### 3) Verify create
1. Call `POST /api/products` with valid payload (without Id).
2. Confirm `201` and generated Id returned.
3. Call `POST /api/products` with client-supplied Id and confirm validation failure Problem Details.

### 4) Verify update
1. Call `PUT /api/products/{id}` with full valid payload.
2. Confirm `200` and updated fields.
3. Call `PUT` with missing required field and confirm validation failure Problem Details.
4. Call `PUT` for non-existent Id and confirm `404` Problem Details.

### 5) Verify delete
1. Call `DELETE /api/products/{id}` for existing product.
2. Confirm `204`.
3. Call `DELETE` again for same Id and confirm `404` Problem Details.

### 6) Verify RFC 7807 payload shape
1. Trigger a validation error (for example, missing `name`).
2. Confirm response content type is `application/problem+json`.
3. Trigger a not-found error (for example, `GET /api/products/999`).
4. Confirm response content type is `application/problem+json`.

## Notes
- Data resets when the process restarts by design (InMemory provider).
- No authentication/authorization in baseline scope.
