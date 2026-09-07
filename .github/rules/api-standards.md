# REST API Standards

## 1. Endpoints & Resource Naming
- Use plural nouns for resources (e.g., `/api/v1/tickets`, `/api/v1/users`).
- Use kebab-case for multi-word paths (e.g., `/api/v1/ticket-categories`).
- Map HTTP methods strictly to semantics:
  - `GET`: Read resource (idempotent, safe).
  - `POST`: Create resource.
  - `PUT`: Full update / replace.
  - `PATCH`: Partial update.
  - `DELETE`: Remove resource.

## 2. HTTP Status Codes
- `200 OK`: Successful read or update.
- `201 Created`: Successful creation (include `Location` header where applicable).
- `204 No Content`: Successful deletion.
- `400 Bad Request`: Validation failure or malformed body.
- `401 Unauthorized`: Missing or invalid authentication token.
- `403 Forbidden`: Authenticated user lacks permission.
- `404 Not Found`: Resource does not exist.
- `409 Conflict`: Business rule violation (e.g., duplicate unique key).

## 3. Error Response Contract
All error responses must return the standard RFC 7807 (Problem Details) format:
```json
{
  "type": "about:blank",
  "title": "Bad Request",
  "status": 400,
  "detail": "Ticket title must not be blank",
  "instance": "/api/v1/tickets",
  "timestamp": "2026-09-07T12:54:00Z"
}
```

## 4. Pagination & Filtering
- Pagination parameters: ?page=0&size=20&sort=createdAt,desc.
- Return paginated payloads with metadata: content, pageNumber, pageSize, totalElements, totalPages.