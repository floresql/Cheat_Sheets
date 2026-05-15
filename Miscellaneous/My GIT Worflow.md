# Git Multi-Remote Feature Workflow Cheat Sheet

## 1. Feature Development & Lifecycle Workflow
Follow this exact sequence to isolate work, track updates, and prevent breaking production.

### Step 1a: Branching & Feature Isolation
Never write code directly on the `main` branch. 

```bash
# Ensure local main matches GitLab main
git checkout main
git pull origin main
```
```bash
# Create and switch to a targeted feature branch
git checkout -b feature/auth-system
```
* **Tip:** Use clear prefixes like `feature/`, `bugfix/`, or `hotfix/` followed by brief descriptions or issue IDs.

### Step 1b: Staging & Granular Commits
Group related changes into logical, micro-commits rather than giant, single saves.

```bash
# Check exactly what changed in your Git Bash workspace
git status
git diff
```
```bash
# Stage specific files instead of bulk adding everything
git add src/auth.js
```
```bash
# Commit with a concise imperative-mood message
git commit -m "feat: implement JWT token validation"
```
* **Tip:** Use atomic commits. If a feature contains both a database tweak and a UI tweak, make two separate commits.

### Step 1c: Merging & Resolving Conflicts
Bring your isolated feature into `main` safely after verifying it passes local checks.

```bash
# Step 1: Update local main from GitLab to catch teammate changes
git checkout main
git pull origin main
```
```bash
# Step 2: Merge the feature branch into main
git merge feature/auth-system
```
```bash
# Step 3: Delete the local feature branch once merged
git branch -d feature/auth-system
```
* **Conflict Tip:** If a conflict happens during `git merge`, run `git status` to find conflicting files. Open them, look for the `<<<<<<<` and `>>>>>>>` markers, resolve the code, then run `git add .` and `git commit` to complete the merge.

## 2. Multi-Remote Deployment Execution
Follow this dual-push pipeline to ensure GitLab holds the definitive history before production runs the live code.

```bash
# Step 1: Push your updated main branch to GitLab (Origin)
git checkout main
git push origin main
```
* **Note:** Pushing to GitLab saves the codebase backup, logs history, and shares updates with your team.

```bash
# Step 2: Deploy verified code directly over the network to the production server (Prod)
git push prod main
```
* **Note:** Pushing to `prod` triggers the network-based `post-receive` script automatically. This updates the live directory immediately.
* **Safety Warning:** Never force push (`git push -f`) to the `prod` remote. Force pushing rewritten history can break files on the live server.
