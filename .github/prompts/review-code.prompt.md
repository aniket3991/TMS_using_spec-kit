## Perform a rigorous code review adhering to project rules
Review the provided code or current diff against the project standards:

1. **Architecture & Design:** Check compliance with `.github/rules/java-springboot.md` (no field injection, no business logic in controllers, proper DTO usage).
2. **REST Standards:** Verify alignment with `.github/rules/api-standards.md` (HTTP methods, status codes, error handling).
3. **Security & Performance:** Check for injection risks, missing input validations, potential N+1 queries, and missing database indexes.
4. **Code Quality:** Identify dead code, code smells, and violation of Clean Code principles.

**Output Format:**
- **Summary:** Quick 2-3 sentence verdict.
- **Critical Issues:** Must-fix bugs, architectural violations, or security vulnerabilities.
- **Suggestions:** Minor improvements and refactorings.
- **Code Fixes:** Concrete replacement snippets for the identified issues.