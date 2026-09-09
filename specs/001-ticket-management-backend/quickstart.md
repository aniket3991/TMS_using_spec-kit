# Quickstart Validation Guide

## Prerequisites

- Java 21
- Maven Wrapper from `backend/mvnw`
- PostgreSQL available locally, or Docker for Testcontainers
- Environment configuration for the datasource; do not commit credentials

## Start the backend

From the repository root:

```bash
cd backend
./mvnw spring-boot:run
```

Open Swagger UI at `http://localhost:8080/swagger-ui/index.html` and compare the generated endpoints with [contracts/openapi.yaml](contracts/openapi.yaml).

## Validate the lifecycle

1. `POST /api/v1/tickets` with a valid title and description. Expect `201`, generated `id`, status `OPEN`, and timestamps.
2. `GET /api/v1/tickets/{id}`. Expect ticket attributes only; no comments collection and no persistence entity fields.
3. `PUT /api/v1/tickets/{id}` with valid title, description, and optional assignee. Expect editable fields updated while status and `createdAt` remain unchanged.
4. `PATCH /api/v1/tickets/{id}/status` through `IN_PROGRESS`, `RESOLVED`, and `CLOSED`; verify the two allowed cancellation paths from `OPEN` and `IN_PROGRESS`.
5. Attempt a terminal or otherwise unlisted transition. Expect `409` with `INVALID_STATUS_TRANSITION` and unchanged status.

## Validate search and comments

1. Create tickets with different titles, descriptions, and statuses.
2. Call `GET /api/v1/tickets?page=0&size=10&keyword=login&status=OPEN`; verify both filters apply and metadata is present.
3. Call `POST /api/v1/tickets/{id}/comments` with valid content, then `GET /api/v1/tickets/{id}/comments?page=0&size=10`; expect a created comment and a paginated chronological collection.
4. Use an unknown ticket id for details, updates, status, and comment creation. Expect `404` and no mutation.

## Validate boundaries and errors

- Titles of 4 and 151 characters, blank descriptions, blank comment content, and 1001-character comments return `400` with field errors.
- Unknown status values and page sizes outside `1..100` return `400`.
- Missing or malformed request bodies return `400`.
- Every error includes the stable structured fields described in the OpenAPI contract and exposes no stack trace or database detail.

## Automated checks

```bash
cd backend
./mvnw test
```

The suite should include pure JUnit/Mockito service tests, `@WebMvcTest` MockMvc contract tests, and `@DataJpaTest` PostgreSQL/Testcontainers repository tests. The concurrent transition test must demonstrate that an optimistic-lock loser receives `409` and cannot overwrite the winning status.
