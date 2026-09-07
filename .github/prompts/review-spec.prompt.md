## Audit an OpenAPI specification against repository API standards

Review the target OpenAPI YAML/JSON definition against `.github/rules/api-standards.md` and `.github/skills/documentation/api-docs.md`.

Verify that:
1. All paths follow kebab-case and plural noun conventions.
2. HTTP methods match the intended action semantics.
3. Every operation includes `operationId`, `summary`, and comprehensive schema definitions.
4. Standard error responses (`400`, `401`, `403`, `404`, `500`) reference the RFC 7807 error schema.
5. Example payloads are supplied for all schemas.

**Output Format:**
- List compliance violations with exact path and line references.
- Provide the corrected OpenAPI YAML snippet.