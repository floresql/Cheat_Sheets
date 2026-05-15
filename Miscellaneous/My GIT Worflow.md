# Git Multi-Remote Feature Workflow Cheat Sheet

An absolute reference guide for isolating features, managing commits, and executing safe deployments across **GitLab (Origin)** and your **Windows Network Server (Prod)**.

---

## Fundamental Golden Rules
1. **Never write code directly on `main`.**
2. **Always pull** from GitLab before starting a new feature branch.
3. **Always push to GitLab (`origin`)** before deploying to the production server (`prod`).

---

## 1. Feature Development Lifecycle

Follow this exact sequence to isolate your work, track updates, and protect production.

### Step A: Branching & Isolation
```bash
# 1. Switch to main and sync with the latest remote team changes
git checkout main
git pull origin main

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

### Step C: Merging & Syncing
```bash
# 1. Head back to main and catch up with GitLab once more
git checkout main
git pull origin main

# 2. Merge your completed feature branch locally
git merge feature/auth-system

# 3. Safely wipe out the local feature branch once it is merged
git branch -d feature/auth-system
```
> 💥 **Conflict Resolution:** If a conflict breaks your merge, run `git status` to find the problem files. Look for the `<<<<<<<` and `>>>>>>>` markers, clean up the conflicting code, then finalize with `git add .` and `git commit`.

---
<BR>

## 2. Multi-Remote Deployment

Execute this dual-push pipeline to ensure your code history is completely safely stored before updating the live ecosystem.

```bash
# Pipeline Step 1: Backup and share your history with the team on GitLab
git checkout main
git push origin main

# Pipeline Step 2: Push directly to the network share to trigger the server checkout script
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
git fetch origin
git reset --hard origin/main
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
