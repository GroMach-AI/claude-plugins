# Conventional Commits Reference

## Format

```
<type>(<scope>): <description>

[optional body]
```

## Common Types

- **feat**: New feature or functionality
- **fix**: Bug fix
- **docs**: Documentation changes only
- **style**: Code style/formatting (no logic changes)
- **refactor**: Code restructuring without changing behavior
- **perf**: Performance improvements
- **test**: Adding or modifying tests
- **build**: Build system or dependencies
- **ci**: CI/CD configuration changes
- **chore**: Routine tasks, maintenance

## Scope (Optional)

The scope provides context about what part of the codebase is affected:
- Component name: `(auth)`, `(api)`, `(ui)`
- Feature area: `(billing)`, `(dashboard)`, `(workflow)`
- File/module: `(keyword-analyzer)`, `(logger)`

## Description

- Use imperative mood ("add" not "added" or "adds")
- Keep under 50-72 characters
- Don't capitalize first letter
- No period at the end
- Focus on **what** changed and **why**, not implementation details

## Examples

```
feat(auth): add Google OAuth integration
fix(api): resolve race condition in keyword mining
docs(readme): update installation instructions
refactor(billing): simplify credit calculation logic
perf(rag): optimize vector similarity search
test(workflow): add unit tests for article generation
```

## Body Guidelines (Optional)

- Separate from description with a blank line
- Explain **why** the change was made
- Describe **what** was changed at a high level
- Keep lines under 72 characters
- Can include multiple paragraphs

## Breaking Changes

If a commit introduces breaking changes, add `BREAKING CHANGE:` in the body or append `!` after type/scope:

```
feat(api)!: change article generation endpoint structure

BREAKING CHANGE: The /api/articles endpoint now returns a different response format.
```
