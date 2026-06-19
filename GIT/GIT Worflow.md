# My Git Workflow Cheat Sheet

An absolute reference guide for isolating features, managing team code reviews via GitLab, and executing safe deployments to our **Windows Network Server (Prod)**.

---

## Fundamental Golden Rules
1. **Never write code directly on `main`.**
2. **Always pull** from GitLab (`dev`) before starting a new feature branch.
3. **Never merge locally.** All feature branches must be merged via a GitLab Merge Request (MR) after a peer review.
4. **Always push to GitLab (`dev`)** and pass code review before deploying to the production server (`prod`).

---

## 1. Feature Development Lifecycle

Follow this exact sequence to isolate your work, collaborate via code reviews, and safely update production.

### Step A: Branching & Isolation
```bash
# 1. Switch to main and sync with the latest remote team changes
git checkout main
git pull dev main

# 2. Spin up a fresh, isolated feature branch
git checkout -b feature/auth-system
```
> 💡 **Branch Naming Tip:** Keep history organized by prefixing branch names: `feature/xyz`, `bugfix/xyz`, or `hotfix/xyz`.

### Step B: Staging & Granular Commits
```bash
# 1. Inspect what files were modified or created
git status
git diff

# 2. Stage specific, logical file blocks instead of dumping everything
git add src/auth.js

# 3. Save your progress with a clear, imperative commit message
git commit -m "feat: implement JWT token validation"
```
> 💡 **Commit Tip:** Aim for *atomic commits*. If a feature contains both a database change and a layout change, split them into two separate commits.

### Step C: Pushing & GitLab Merge Request (Code Review & Approval)
```bash
# Option 1: Native Git push that automatically builds your GitLab MR
git push dev -o merge_request.create -o merge_request.target=main -o merge_request.reviewer="teammate_username"

# Option 2: Basic push and manual setup
git push dev feature/auth-system
#    - Open GitLab in your browser and click "Create Merge Request".
#    - Assign a teammate to review your code.
```
> 🔄 **Handling Mid-Review Updates:** If a reviewer asks for changes, or if `main` moves ahead while you wait, update your branch locally and push again:
```bash
# Sync your branch with any new updates from other team members
git pull dev main

# Make your fixes, commit, and push (the MR updates automatically)
git add .
git commit -m "fix: address PR review feedback on token expiration"
git push dev feature/auth-system
```

### Step D: The Merge & Local Cleanup
> ⚠️ **CRITICAL:** Do not merge locally. Once approved, click **"Squash and Merge"** directly inside the GitLab web interface. This condenses your development commits into one clean historical entry on `main`.

```bash
# Once merged on GitLab, clean up your local computer workspace:
git checkout main
git pull dev main
git branch -d feature/auth-system
```

---
<BR>

## 2. Multi-Remote Deployment Pipeline

Once your Merge Request is successfully merged into `main` on GitLab, execute this sequence to sync your local environment and deploy the final code to production.

```bash
# 1. Pull the newly merged and squashed main branch down from GitLab
git checkout main
git pull dev main

# 2. Push directly to the network share to trigger the server checkout script
git push prod main
```

> ⚠️ **CRITICAL WARNING:** Never run a force push (`git push -f`) against the `prod` remote. Forcing rewritten history can break files actively serving live web traffic.

---
<BR>

## 3. Semantic Commit Examples

Using standard, structured commit message prefixes makes your repository history scannable and easy to read.




| Prefix | Core Purpose | Concrete Git Bash Example |
| :--- | :--- | :--- |
| **`feat:`** | Introducing a brand new asset or function | `git commit -m "feat: add user profile picture upload fallback"` |
| **`fix:`** | Repairing an error, crash, or flawed logic | `git commit -m "fix: resolve memory leak on connection close"` |
| **`docs:`** | Editing documentation, READMEs, or comments | `git commit -m "docs: add environment setup variables to readme"` |
| **`style:`**| Formatting, spacing, or fixing code styling | `git commit -m "style: run prettier formatter on layout templates"` |
| **`refactor:`**| Rewriting logic without altering functional specs | `git commit -m "refactor: simplify parsing loop inside file reader"` |
| **`test:`** | Adding missing unit tests or test coverage suites | `git commit -m "test: add suite for login endpoint timeout rules"` |

---
<BR>

## 4. Disaster Recovery & Emergency Kits

Quick commands to wipe out local workspace mistakes or roll back file changes.

```bash
# Nuke all local unstaged modifications in the current working directory
git checkout -- .

# Unstage a file added by mistake while keeping your actual code edits
git reset HEAD filename.ext

# Quick-fix the message or contents of your last un-pushed commit
git commit --amend -m "fix: new exact message description"

# Hard reset your entire local branch to perfectly mirror GitLab
git fetch dev
git reset --hard dev/main
```

---
<BR>

## 5. Stashing Workspace Cache

Safely tuck away unfinished progress without making a messy, incomplete commit.

```bash
# 1. Shove your messy, uncommitted code down onto the stash stack
git stash -m "wip: incomplete layout adjustment"

# 2. View your stack of saved temporary workspaces
git stash list

# 3. Pull your changes back out of storage and wipe the stash record
git stash pop
```

---
<BR>

## 6. History Logs & Inspection

```bash
# Read a highly compressed, beautifully structured branch/commit tree
git log --oneline --graph --decorate

# Inspect exactly what changes live in your staged area vs your files
git diff --staged
```
