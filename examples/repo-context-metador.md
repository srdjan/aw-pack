## Project

Metador is a minimal, composable type algebra for building metadata systems, written in TypeScript for Deno. Package: `@metador/core` (published to JSR).

## Architecture

- **L1 Type Algebra**: `src/types.ts`, `src/constructors.ts` - closed union of 11 TypeExpression kinds (Primitive, Literal, Opaque, List, Map, Tuple, Optional, Obj, Union, Intersection, Reference)
- **L1.5 Capabilities**: `src/capabilities.ts` - Haskell-style typeclasses that attach behavioral contracts to types
- **DSL**: `src/dsl_types.ts`, `src/dsl_capabilities.ts`, `src/dsl_schema.ts`, `src/prelude.ts` - public API via `t`, `cap`, `schema()`, and `prelude` namespaces
- **Derivation**: `src/derive.ts`, `src/dsl_derive.ts` - type-to-type transforms (omit, pick, partial, required, extend)
- **Fold**: `src/fold.ts` - catamorphism over the type algebra, used by codegen and persistence
- **Diff**: `src/diff.ts` - schema evolution and backwards compatibility checking
- **Codegen**: `src/codegen.ts` - TypeScript code generation from type definitions
- **JSON Schema**: `src/json_schema.ts` - JSON Schema (draft 2020-12) generation
- **CLI**: `cli/` - JSON-in/JSON-out command-line interface with 7 commands
- **Persistence**: `src/persistence.ts` - schema validation and JSON serialization

## Component Labels

type-algebra, capabilities, dsl, codegen, schema-evolution, cli

## Conventions and Build Commands

Conventions:
- All types immutable (`readonly` throughout) and plain data (no classes)
- Error handling via Result types (`ParseResult`) and error arrays, never thrown exceptions
- Exhaustive pattern matching on `kind` discriminants for the closed TypeExpression union
- No use of `any` type - use `unknown` with proper type narrowing
- New TypeExpression kinds must be integrated in all folds, codegen, JSON Schema, diff, persistence, and CLI

Build: `deno task check`
Test: `deno task test`
CLI: `deno task cli -- <command>`
