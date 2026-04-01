# Data Model: Baseline Product Management API

## Entity: Product
- Purpose: Represents an inventory item managed through CRUD endpoints.

### Fields
- Id: integer, server-generated, unique, immutable after creation.
- Name: string, required, non-empty.
- Description: string, optional text description.
- Price: decimal, required, must be greater than 0.
- Quantity: integer, required, must be greater than or equal to 0.

### Validation Rules
- Name is required.
- Price > 0.
- Quantity >= 0.
- Client-supplied Id in create request is invalid and rejected.
- Full PUT update requires all required fields.

### Lifecycle
- Created: Product is inserted with server-generated Id.
- Updated: Existing product is fully replaced by valid payload.
- Deleted: Product is removed from in-memory store.

### State Notes
- No soft-delete state.
- No archived/inactive state in baseline scope.

## Relationships
- None in baseline scope.
