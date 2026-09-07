# Testing Guidelines

## Backend (Spring Boot)
- **Frameworks:** JUnit 5, Mockito, AssertJ, Testcontainers (for PostgreSQL).
- **Unit Tests:**
  - Mock all downstream dependencies using `@Mock` and `@InjectMocks`.
  - Do not spin up Spring Context (`@SpringBootTest`) for pure business logic tests.
  - Follow the **AAA** pattern (Arrange, Act, Assert).
- **Integration/Slice Tests:**
  - Use `@WebMvcTest` for controller routing, serialization, and status code checks.
  - Use `@DataJpaTest` with Testcontainers for repository queries.

## Frontend (React)
- **Frameworks:** Vitest/Jest, React Testing Library (RTL).
- **Standards:**
  - Test user interactions over implementation details.
  - Query elements primarily by accessibility roles (`getByRole`, `findByRole`) or labels.
  - Mock network calls using MSW (Mock Service Worker).

## Coverage & Quality
- Focus tests on edge cases: null handling, boundary conditions, unauthorized flows, and error responses.
- Ensure all tests are deterministic and independent (no shared mutable state).