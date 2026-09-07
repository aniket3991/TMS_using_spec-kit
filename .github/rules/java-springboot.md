# Java & Spring Boot Guidelines

## 1. Architecture & Layering
- Follow strict layered architecture: `Controller -> Service -> Repository -> Database`.
- **Controllers:** Light; handle HTTP requests, input validation, and delegate to services. Never place business logic here.
- **Services:** Manage transactions (`@Transactional`), business rules, and mapping between entities and DTOs.
- **Repositories:** Spring Data JPA interfaces; use JPQL or specifications for complex queries.

## 2. Dependency Injection & State
- Always use **constructor injection** with `final` fields (or `@RequiredArgsConstructor` via Lombok).
- Never use field injection (`@Autowired` on fields).
- Keep services stateless.

## 3. Data Transfer & Persistence
- Never expose JPA `@Entity` classes directly to controllers or clients. Always map to/from DTOs (using MapStruct or manual mappers).
- Use `records` for immutable DTOs and request/response payloads.
- Use Jakarta validation annotations (`@NotNull`, `@NotBlank`, `@Size`, etc.) on incoming request DTOs.

## 4. Exception Handling
- Use a single centralized `@RestControllerAdvice` handling domain-specific exceptions.
- Throw custom runtime exceptions (e.g., `TicketNotFoundException`, `UnauthorizedAccessException`) rather than generic `RuntimeException`.