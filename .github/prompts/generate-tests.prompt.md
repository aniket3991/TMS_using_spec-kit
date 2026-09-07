## Generate unit and integration test suites for given code

Generate a comprehensive test suite for the provided class or component based on `.github/rules/testing.md`.

## Requirements:
1. **For Spring Boot Services:**
   - Use JUnit 5 and Mockito (`@ExtendWith(MockitoExtension.class)`).
   - Mock all dependencies and verify interactions.
   - Cover positive, negative, and edge cases (e.g., entity not found, validation fail).
2. **For Spring Boot Controllers:**
   - Use `@WebMvcTest` and `MockMvc` to verify HTTP status codes, headers, and JSON serialization.
3. **For React Components:**
   - Use React Testing Library and Vitest/Jest.
   - Test user interactions and assertions via accessible roles (`getByRole`).
4. Follow the **Arrange-Act-Assert (AAA)** pattern with clean, readable test method names (e.g., `shouldReturnTicketWhenValidIdProvided`).