# Ticket Management System — Workspace Instructions

You are an expert full-stack engineer working on this repository. Always align your solutions with the architecture and standards defined below.

## Architecture Context
- **Pattern:** Monorepo with an API-first design.
- **Backend:** Spring Boot (Java 21/17), Spring Data JPA, PostgreSQL.
- **Frontend:** React with TypeScript, Vite, and modern state management.
- **API Spec:** Central OpenAPI 3.x specification driving code generation.

## Enforced Steering Standards
Before generating, refactoring, or reviewing code, always follow:
- **Backend Guidelines:** `.github/rules/java-springboot.md`
- **Testing Guidelines:** `.github/rules/testing.md`
- **API Standards:** `.github/rules/api-standards.md`
- **Documentation:** `.github/skills/documentation/api-docs.md` and `.github/skills/documentation/code-comments.md`

## Prompt Commands Available
- To review code: `.github/prompts/review-code.prompt.md`
- To review API specs: `.github/prompts/review-spec.prompt.md`
- To generate test suites: `.github/prompts/generate-tests.prompt.md`

## Codebase Intelligence (Graphify)
- A pre-built knowledge graph is generated under `graphify-out/graph.json`.
- Before reading multiple Java files to understand dependencies or entity mappings, inspect `graphify-out/GRAPH_REPORT.md` or query the AST knowledge graph.