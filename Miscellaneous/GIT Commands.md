# GIT Cheat Sheet

## 0.  Stuff I'm using now
```bash
# Push to Prod
git push prod dev:main
```

<BR>

## 1. Git Command Reference

### Basics & Configuration
```bash
# Setup identity
git config --global user.name "Your Name"
git config --global user.email "mail@example.com"

# Initialize or Clone
git init <directory>               # Create a new local repo
git clone <url>                    # Clone a remote repo
git status                         # View staged/unstaged changes
```

### Branching & Merging
```bash
# Inspection & Listing
git branch                         # List your local branches (current marked with *)
git branch -r                      # List all remote tracking branches
git branch -a                      # List all branches (both local and remote)
git branch -v                      # List local branches with latest commit message (verbose)
git branch -vv                     # Show local branches with extra details and upstream tracking
git branch --show-current          # Print only the name of the current branch

# Actions & Merges
git switch -c <name>               # Create and switch to new branch
git switch <name>                  # Switch to existing branch
git merge <branch>                 # Merge <branch> into current branch
git branch -d <branch>             # Delete a merged local branch
```

### Remote Synchronization
```bash
# Manage Remotes
git remote add <name> <url>        # Link local repo to a remote source
git remote add gitlab git@gitlab.com:username/repo.git # Add GitLab as a remote
git remote add production ssh://user@your-server.com # Add your remote server as a remote
git remote remove <remote_name>    # Remove a defined remote configuration

# Sync Data
git fetch <remote>                 # Download objects/refs from remote
git pull <remote> <branch>         # Fetch and immediately merge
git push -u origin <branch>        # Push and set upstream tracking
git push gitlab main               # Push specific branch to GitLab remote
git push origin --delete <branch>  # Delete remote branch
git push <remote> --tags           # Push local tags to remote
```

### Undoing & Rewriting History
```bash
git add <file>                     # Stage changes
git commit -m "message"            # Commit staged changes
git commit --amend                 # Edit last commit or add staged changes to it
git reset <file>                   # Unstage <file>, keep workspace changes
git revert <commit>                # Create a new commit that undoes <commit>
git stash                          # Temporarily shelf uncommitted changes
git stash pop                      # Bring stashed changes back
```

---

## 2. Reset Modes & Inspection



| Command | Effect on Staging | Effect on Working Directory |
| :--- | :--- | :--- |
| `git reset` | Resets to match last commit | Changes are KEPT |
| `git reset --hard` | Resets to match last commit | Changes are DELETED |
| `git reset <commit>` | Resets to specific commit | Changes are KEPT |
| `git reset --hard <commit>` | Resets to specific commit | Changes are DELETED |

### Git Log (Inspection)
* **`git log --oneline`**: Condense history to single lines.
* **`git log --graph --decorate`**: Visual text-based branch graph.
* **`git log -<limit>`**: Show only the last N commits (e.g., `git log -5`).
* **`git log --grep="pattern"`**: Search commit messages for a pattern.

---

## 3. General Best Practices
* **Keep branches short-lived**: Focus on a single feature or fix per branch.
* **Pull frequently**: Reduce merge conflicts by staying updated with `develop`.
* **Review before merging**: Always test and review code before it hits `main`.
* **Never `push --force`**: Unless you are 100% sure and working on a private feature branch.
* **Use `.gitignore`**: Ensure `.env`, `node_modules`, and OS files (like `.DS_Store`) are never tracked.
