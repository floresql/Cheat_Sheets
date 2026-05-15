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

## 3. Best Practice Commit Examples
Write clear, clean, and scannable history by using standard structured semantic message prefixes.


| Prefix | Use Case | Clear Example |
| :--- | :--- | :--- |
| **`feat:`** | Creating a completely new capability or component | `git commit -m "feat: add user profile picture upload fallback"` |
| **`fix:`** | Repairing a bug or fixing an application crash | `git commit -m "fix: resolve memory leak on connection close"` |
| **`docs:`** | Editing files like README.md, comments, or wikis | `git commit -m "docs: add environment setup variables to readme"` |
| **`style:`** | Formatting, adding whitespace, or fixing missing semicolons | `git commit -m "style: run prettier formatter on layout templates"` |
| **`refactor:`**| Rewriting logic without modifying behavior or specs | `git commit -m "refactor: simplify parsing loop inside file reader"` |
| **`test:`** | Introducing missed unit tests or adding automated coverage| `git commit -m "test: add suite for login endpoint timeout rules"` |

## 4. Disaster Recovery & Emergency Operations
Quick commands to save your progress or undo local workspace mistakes.

```bash
# Discard all local unstaged modifications in the folder
git checkout -- .

# Unstage a file you added by mistake but keep the code intact
git reset HEAD filename.ext

# Modify the message or contents of your last un-pushed commit
git commit --amend -m "fix: new exact message description"

# Hard reset your local workspace to match GitLab state completely
git fetch origin
git reset --hard origin/main
```

## 5. Stashing Workspaces
Safely store unfinished feature progress without forcing a half-baked commit.

```bash
# Save and hide local modifications onto the stash stack
git stash -m "wip: incomplete layout adjustment"

# See your list of active stashes
git stash list

# Re-apply the most recently stashed changes back into your workspace
git stash pop
```

## 6. History Logs & Inspection
Quick shortcuts to inspect your work layout inside Git Bash.

```bash
# Read a highly compressed, single-line commit history graph
git log --oneline --graph --decorate

# Inspect changes inside your staged area vs your actual code files
git diff --staged
```
