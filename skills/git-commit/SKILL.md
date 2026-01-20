---
name: git-commit
description: Create well-structured git commits using Conventional Commits format. Use this skill when the user asks to commit changes, create a commit, review changes before committing, check what changed, or prepare to commit. Also activates for related tasks like analyzing staged/unstaged changes, drafting commit messages, or understanding recent commit history.
---

# Git Commit

Systematically create high-quality git commits following Conventional Commits format.

## Commit Workflow

Follow these steps in order when creating commits:

### 1. Understand Current State

Run these commands in parallel to understand what will be committed:

```bash
git status
git diff          # Unstaged changes
git diff --staged # Staged changes
git log -5 --oneline  # Recent commits for context
```

### 2. Analyze Changes

Review the diff output to understand:
- What files changed
- What functionality was added, modified, or removed
- Why these changes were made (based on context)
- Whether changes represent a feature, fix, refactor, etc.

**Important**: Never commit files that likely contain secrets (.env, credentials.json, secrets.yaml, etc.). Warn the user if they request to commit such files.

### 3. Draft Commit Message

Create a Conventional Commit message following this format:

```
<type>(<scope>): <description>
```

**Type selection**:
- `feat`: New feature or functionality
- `fix`: Bug fix
- `refactor`: Code restructuring without changing behavior
- `perf`: Performance improvements
- `docs`: Documentation changes only
- `style`: Formatting changes (no logic changes)
- `test`: Adding or modifying tests
- `chore`: Routine tasks, maintenance
- `build`: Build system or dependencies
- `ci`: CI/CD configuration

**Scope** (optional): Component, feature area, or module affected (e.g., `auth`, `api`, `workflow`)

**Description**:
- Use imperative mood: "add" not "added"
- Keep concise (under 50-72 characters)
- Don't capitalize first letter
- No period at the end
- Focus on **what** and **why**, not implementation details

For detailed guidance, see [references/conventional-commits.md](references/conventional-commits.md).

### 4. Stage and Commit

Stage relevant files and create the commit:

```bash
git add <files>
git commit -m "type(scope): description"
```

**Using heredoc for multi-line messages**:

```bash
git commit -m "$(cat <<'EOF'
feat(auth): add Google OAuth integration

Implemented OAuth2 flow with Google provider to allow
users to sign in with their Google accounts.
EOF
)"
```

### 5. Verify

After committing, verify success:

```bash
git status
git log -1  # Show the commit just created
```

## Common Patterns

### Simple Feature Addition

```
User: "Commit the new login button I just added"

Workflow:
1. Check git status and diff
2. Identify this as a new feature
3. Draft: feat(auth): add login button to navbar
4. Stage files: git add components/navbar.tsx
5. Commit and verify
```

### Bug Fix

```
User: "Create a commit for the race condition fix"

Workflow:
1. Review changes with git diff
2. Identify this as a bug fix
3. Draft: fix(workflow): resolve race condition in keyword mining
4. Add context in body if needed
5. Stage, commit, verify
```

### Reviewing Before Commit

```
User: "What changes do I have? Should I commit them?"

Workflow:
1. Run git status and git diff
2. Analyze and explain changes to user
3. Suggest logical groupings if multiple unrelated changes exist
4. Ask user how they want to proceed
5. Create commits as requested
```

## Pre-commit Hook Handling

If a commit fails due to a pre-commit hook:

**Hook REJECTED the commit** (non-zero exit):
- Fix the issue identified by the hook
- Create a NEW commit (never amend)

**Commit SUCCEEDED but hook auto-modified files**:
- Review what the hook changed
- Stage the auto-modified files: `git add <files>`
- Amend the commit: `git commit --amend --no-edit`
- Only do this for commits you just created, not existing commits

When in doubt, create a new commit instead of amending.

## Git Safety Rules

- **Never** run destructive commands (force push, hard reset) unless explicitly requested
- **Never** skip hooks with --no-verify unless explicitly requested
- **Never** update git config without user permission
- **Never** amend commits that have been pushed to remote
- **Never** force push to main/master branches

## Multi-file Changes

When there are changes to multiple unrelated areas:

1. Review all changes
2. Suggest logical groupings (e.g., separate feature changes from bug fixes)
3. Create separate commits for each logical group
4. Use appropriate type and scope for each commit

Example:
```
# Changes to auth + unrelated docs update
git add lib/auth.ts
git commit -m "feat(auth): add session timeout handling"

git add README.md
git commit -m "docs(readme): update installation steps"
```
