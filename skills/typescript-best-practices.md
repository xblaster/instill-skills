# TypeScript Best Practices

## Type Safety
- Always use explicit type annotations for function parameters and return types
- Prefer interfaces over types for object shapes
- Enable strict mode in tsconfig.json

## Code Organization
- Group related types in dedicated files
- Use namespaces for large collections of types
- Keep utility functions in separate files

## Naming Conventions
- Use PascalCase for classes and interfaces
- Use camelCase for variables, functions, and properties
- Use UPPER_SNAKE_CASE for constants

## Common Patterns
- Use readonly for immutable properties
- Prefer const over let
- Use strict null checks (strictNullChecks: true)
- Avoid any type - use unknown when uncertain
