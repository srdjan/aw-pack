## Project

<!-- Replace this section with your project's identity. Example: -->
<!-- MyApp is a real-time collaboration platform written in TypeScript/Node.js. Package: @myorg/myapp. -->
Read the repository's README.md to understand the project identity, purpose, and tech stack.
If a CLAUDE.md or AGENTS.md file exists, read it for additional project context.

## Architecture

<!-- Replace this section with your project's architectural layers and file paths. Example: -->
<!-- - **API Layer**: `src/api/` - REST endpoints and middleware -->
<!-- - **Domain**: `src/domain/` - business logic and models -->
<!-- - **Database**: `src/db/` - migrations, queries, and repositories -->
<!-- - **Frontend**: `app/` - React components and pages -->
Explore the repository structure to identify major modules and their relationships.
Read any CLAUDE.md, ARCHITECTURE.md, CONTRIBUTING.md, or docs/ directory for documented architecture.
If no architecture documentation exists, infer the structure from the directory layout.

## Component Labels

<!-- Replace this section with project-specific labels that map to your architecture. Example: -->
<!-- api, frontend, database, auth, cli, infra -->
When categorizing by component, use labels that match the project's module structure.
Common patterns: api, frontend, backend, database, auth, cli, docs, infra, tests.
If the project has no established component labels, use directory-based labels.

## Conventions and Build Commands

<!-- Replace this section with your project's coding conventions and commands. Example: -->
<!-- Conventions: strict TypeScript (no any), functional style, Result types for errors. -->
<!-- Build: npm run build -->
<!-- Test: npm test -->
<!-- Lint: npm run lint -->
<!-- Type-check: npx tsc --noEmit -->
Check for package.json scripts, Makefile targets, deno.json tasks, Cargo.toml,
pyproject.toml, or Gemfile to discover the project's build and test commands.
Read CLAUDE.md, CONTRIBUTING.md, .editorconfig, or linter configs for coding conventions.
If no conventions are documented, check for standard patterns: linting configs (.eslintrc,
.prettierrc, rustfmt.toml, .rubocop.yml), type safety settings (tsconfig.json strict mode),
and test frameworks (jest.config, pytest.ini, .rspec).
