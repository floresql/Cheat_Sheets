# GIT Cheat Sheet

## 1. Workflow Summary (GitLab Flow Inspired)
This workflow uses dedicated branches for development, testing, and production to maintain stability.

### Phase 1: Feature Development
1.  **Branch off `develop`**: Create a descriptive branch (e.g., `feature/add-login`) from the latest `develop`.
2.  **Commit Frequently**: Make small, logical commits. Use [Conventional Commits](#conventional-commit-prefixes).
3.  **Push**: Push the feature branch to the remote repository for visibility.

### Phase 2: Staging & UAT
1.  **Merge to `develop`**: Manually merge the feature branch into `develop` for code reviews.
2.  **Merge to `main`**: When features are ready for testing, merge `develop` into `main`.
3.  **Automated UAT**: Merging to `main` triggers a `post-receive` hook for automatic UAT deployment.

### Phase 3: Production & Cleanup
1.  **Manual Production Deployment**: Run the PowerShell deployment script (requires manual confirmation).
2.  **Cleanup**: Delete feature branches locally and remotely after a successful production push.

---

## 2. Conventional Commit Prefixes
Use these prefixes to categorize your changes:


| Prefix | Description |
| :--- | :--- |
| `feat:` | A new feature (e.g., `feat: add login validation`) |
| `fix:` | A bug fix (e.g., `fix: resolve logout timeout`) |
| `docs:` | Documentation only changes |
| `refactor:` | Code change that neither fixes a bug nor adds a feature |
| `test:` | Adding missing tests or correcting existing tests |
| `chore:` | Updating build tasks, package manager configs, etc. |

---

## 3. Git Command Reference

### Basics & Configuration
```bash
# Setup identity
git config --global user.name "Your Name"
git config --global user.email "mail@example.com"

# Initialize or Clone
git init <directory>       # Create a new local repo
git clone <url>            # Clone a remote repo
git status                 # View staged/unstaged changes
```

### Branching & Merging
```bash
git branch                 # List branches
git switch -c <name>       # Create and switch to new branch
git switch <name>          # Switch to existing branch
git merge <branch>         # Merge <branch> into current branch
git branch -d <branch>     # Delete a merged local branch
```

### Remote Synchronization
```bash
git remote add <name> <url> # Link local to remote
git fetch <remote>          # Download objects/refs from remote
git pull <remote> <branch>  # Fetch and immediately merge
git push -u origin <branch> # Push and set upstream tracking
git push origin --delete <branch> # Delete remote branch
git push <remote> --tags    # Push local tags to remote
```

### Undoing & Rewriting History
```bash
git add <file>             # Stage changes
git commit -m "message"    # Commit staged changes
git commit --amend         # Edit last commit or add staged changes to it
git reset <file>           # Unstage <file>, keep workspace changes
git revert <commit>        # Create a new commit that undoes <commit>
git stash                  # Temporarily shelf uncommitted changes
git stash pop              # Bring stashed changes back
```

---

## 4. Reset Modes & Inspection


| Command | Effect on Staging | Effect on Working Directory |
| :--- | :--- | :--- |
| `git reset` | Resets to match last commit | Changes are KEPT |
| `git reset --hard` | Resets to match last commit | Changes are DELETED |
| `git reset <commit>` | Resets to specific commit | Changes are KEPT |
| `git reset --hard <commit>` | Resets to specific commit | Changes are DELETED |

### Git Log (Inspection)
*   **`git log --oneline`**: Condense history to single lines.
*   **`git log --graph --decorate`**: Visual text-based branch graph.
*   **`git log -<limit>`**: Show only the last N commits (e.g., `git log -5`).
*   **`git log --grep="pattern"`**: Search commit messages for a pattern.

---

## 5. General Best Practices
*   **Keep branches short-lived**: Focus on a single feature or fix per branch.
*   **Pull frequently**: Reduce merge conflicts by staying updated with `develop`.
*   **Review before merging**: Always test and review code before it hits `main`.
*   **Never `push --force`**: Unless you are 100% sure and working on a private feature branch.
*   **Use `.gitignore`**: Ensure `.env`, `node_modules`, and OS files (like `.DS_Store`) are never tracked.
