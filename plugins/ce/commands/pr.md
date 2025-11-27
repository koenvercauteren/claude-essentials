---
description: Create a pull request with auto-generated description
argument-hint: "[base-branch]"
allowed-tools: Bash, Read, Grep
---

Create a well-structured pull request for the current branch.

Arguments:

- `$ARGUMENTS`: Optional base branch to merge into (defaults to main/master)

Process:

1. Gather context:
   ```bash
   git status
   git log $(git merge-base HEAD origin/main)..HEAD --oneline
   git diff $(git merge-base HEAD origin/main)..HEAD --stat
   ```

2. Analyze the changes:
   - Review all commits on this branch
   - Understand the overall purpose of the changes
   - Identify the type of change (feature, fix, refactor, etc.)
   - Note any breaking changes

3. Check prerequisites:
   - Ensure all changes are committed
   - Verify branch is pushed to remote
   - Check if tests pass (warn if not)

4. Generate PR content:

   **Title**: Concise summary following conventional format
   - `feat: add user authentication flow`
   - `fix: resolve race condition in data sync`
   - `refactor: simplify payment processing logic`

   **Description** (using this template):
   ```markdown
   ## Summary
   [2-3 sentences explaining what this PR does and why]

   ## Changes
   - [Bullet list of key changes]

   ## Testing
   - [ ] Unit tests added/updated
   - [ ] Manual testing completed
   - [ ] [Other relevant checks]

   ## Notes
   [Any additional context, screenshots, or considerations for reviewers]
   ```

5. Create the PR:
   ```bash
   gh pr create --title "..." --body "..." --base <base-branch>
   ```

6. Report the PR URL and any warnings (failing checks, conflicts, etc.)

If there are uncommitted changes, prompt the user to commit first before creating the PR.
