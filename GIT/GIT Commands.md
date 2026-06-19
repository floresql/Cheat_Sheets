# GIT Cheat Sheet

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

## 1. The Daily Workflow (Stage & Commit)

### Tracking Changes
```bash
git status                           # Check staged, unstaged, and untracked files
git status -s                        # Short, compact version of status
git add <file>                       # Stage a specific file for the next commit
git add .                            # Stage all modified and untracked files
git add -p                           # Interactively stage parts of files (hunks)
```

### Committing & Stashing
```bash
git commit -m "message"              # Commit staged changes with a descriptive message
git commit -am "message"             # Shortcut to stage tracked files and commit in one go
git commit --amend --no-edit         # Add staged changes to last commit without changing message
git stash -u                         # Shelf uncommitted changes, including untracked files
git stash pop                        # Re-apply the last stashed changes and delete them from stash
git stash list                       # View all saved items in your stash stack
```

---

## 2. Team Branching & Merging (GitHub Flow)

### Branch Inspection
```bash
git branch                           # List local branches (* shows current)
git branch -r                        # List remote tracking branches
git branch -a                        # List all local and remote branches
git branch -vv                       # Show local branches, latest commit, and upstream tracking
git branch --show-current            # Print only the name of the active branch
```

### Feature Branching & Modification
```bash
git switch <name>                    # Move to an existing branch
git switch -c <name>                 # Create a new feature branch and switch to it
git branch -m <new-name>             # Rename the current active branch
git branch -m <old-name> <new-name>  # Rename a branch while standing on a different one
git branch -d <branch>               # Delete a fully merged local feature branch
git branch -D <branch>               # Force delete a local branch (loses unmerged work)
```

### Integrating Team Changes
```bash
git merge <branch>                   # Merge <branch> into your current active branch
git merge --abort                    # Stop a conflicted merge and revert back to pre-merge state
git cherry-pick <commit>             # Copy a single specific commit from another branch into yours
git rebase main                      # Reapply your branch commits on top of the latest main branch
```

---

## 3. Remote Synchronization & Deployment

### Syncing with the Team (GitLab Dev)
```bash
git fetch dev --prune                # Download team data and prune deleted remote branches
git pull --rebase dev main           # Get latest team updates from main and rebase your work on top
git push -u dev <feature-branch>     # Push feature branch to GitLab for your teammate to review

git push dev --delete <feature-branch> # Delete feature branch from GitLab after it is merged
```

### Deploying to Production (Server Remote)
```bash
git checkout main                    # Switch to your local production-ready branch
git pull --rebase prod main           # Ensure local main matches the latest reviewed GitLab main
git push prod main                   # Push to prod remote to trigger the server post-receive hook
```

### Workflow: Temporarily Change Tracked Upstream
Use this sequence if you need the literal output of `git status` to temporarily track and align with an alternate remote repository or branch without destroying your primary configuration.
```bash
git branch -u <remote-name>/<branch-name> # 1. Re-bind tracking upstream to alternate remote/branch
git fetch <remote-name>                   # 2. Fetch changes from the alternate target
git status                                #    Check status against the alternate target
git branch -u dev/main                    # 3. Restore original remote tracking target when finished
```

---

## 4. Inspection & History

### Log Navigation
```bash
git log --oneline                    # View history compressed into single lines with short hashes
git log -n 5                         # Limit history output to the last 5 commits
git log --graph --oneline --decorate --all # Visual ASCII text tree of all branches and merges
git log --grep="pattern"             # Search commit messages for specific text string
git log -S "code_string"             # Search through code changes for specific text
git diff                             # Show differences between working directory and staging area
git diff --staged                    # Show differences between staging area and last commit
```

### Time Travel (Safe View)
```bash
git checkout <commit>                # Switch to detached HEAD state to safely test old code
git switch -                         # Jump safely back to your previous active branch
```

---

## 5. Undoing Mistakes & History Rewriting

### Reset Matrices


| Command | Effect on Staging Area | Effect on Working Directory | Safe for Shared Remotes? | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| `git reset <commit>` | Resets to match `<commit>` | Keeps your code files untouched | **No** (Local branch only) | Uncommit changes to edit them |
| `git reset --hard <commit>` | Resets to match `<commit>` | **Destroys** all unstaged files/code | **No** (Destructive) | Throw away unwanted work completely |
| `git revert <commit>` | Creates a new safe commit | Appends changes safely | **Yes** (Safe for team work) | Undo a bug introduced in shared main branch |

### Interactive Cleanup (Do before pushing to dev)
```bash
git commit --amend                   # Open text editor to modify the message of the last commit
git reset HEAD~1                     # Undo the last commit, move changes back to working directory
git rebase -i HEAD~3                 # Interactively squash, edit, or delete the last 3 commits
```

---

## 6. Maintenance & Cache Operations

### Refreshing `.gitignore`
If you add files to `.gitignore` after they have already been tracked, Git will continue to track them. Run this exact sequence to purge the cache and apply your newly updated ignore rules without deleting your actual physical files:
```bash
git rm -r --cached .                 # 1. Unstage all files from the index cache (safe)
git add .                            # 2. Re-index all files while applying new .gitignore rules
git commit -m "Apply .gitignore"     # 3. Commit the cleaned up index tree
```

### Housekeeping
```bash
git clean -fd                        # Force remove all untracked files/directories from work tree
git gc --prune=now                   # Run garbage collection to optimize local storage size
```

---

## 7. General Best Practices for Two-Person Teams
* **Atomic Commits**: Group only related changes into a single commit. Do not mix features with formatting fixes.
* **Pull Before Push**: Always run `git pull --rebase` before running a `git push` to resolve conflicts early.
* **Keep Feature Branches Short**: Merge branches back to your main tracking branch quickly to reduce long-term merge conflict debt with your partner.
* **Never Force Push Shared History**: Do not run `git push --force` on the shared `dev` main or `prod` main. Use `git revert` instead. If you must modify an unmerged feature branch, use `git push --force-with-lease`.
* **Lock Sensitive Data Early**: Ensure `.env`, local configuration files, and heavy dependency directories (like `node_modules` or `vendor/`) are added to `.gitignore` before making your first repository commit.
