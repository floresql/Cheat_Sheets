# Git Multi-Remote Workflow Cheat Sheet (GitLab & Prod Server)

## 1. Production Server Configuration
Set up the bare repository and deployment directory on your remote server-prod.

## On the server
***Make sure you're using UNC Paths with forward slashes for Git compatibility***

```bash
# Create a directory for the live website files
mkdir -p //VM0PWNEROPA6001/NewDirName
```
```bash
# Create a bare Git repository directory
cd "//VM0PWNEROPA6001/GIT_Repos"
mkdir your-project-name.git
cd your-project-name.git
```
```bash
# Initialize the bare repository
git init --bare --shared
git branch -m main
```
```bash
# Create and open the post-receive hook file
nano hooks/post-receive
```

### Post-Receive Hook Script
Paste the following script into the `hooks/post-receive` file:

```bash
#!/bin/bash
# Define deployment targets
TARGET="//VM0PWNEROPA6001/NewDirName"
GIT_DIR="//VM0PWNEROPA6001/GIT_Repos/your-project-name.git"

# Deploy the code to the live directory
mkdir -p \$TARGET
git --work-tree=\(TARGET --git-dir=\)GIT_DIR checkout -f main

# Optional: Add framework specific tasks here
# cd \$TARGET && npm install --production
```

Make the hook script executable and exit:

```bash
chmod +x hooks/post-receive
exit
```

## 2. Local Machine Authentication & Setup
Generate SSH keys locally and add them to GitLab for seamless authentication.

```bash
# Generate a secure SSH key pair
ssh-keygen -t ed25519 -C "your_email@example.com"
```
```bash
# Start the ssh-agent in the background
eval "\$(ssh-agent -s)"
```
```bash
# Add your SSH private key to the agent
ssh-add ~/.ssh/id_ed25519
```
```bash
# Copy the public key to clipboard to paste into GitLab Settings -> SSH Keys
cat ~/.ssh/id_ed25519.pub
```

Configure your local Git repository remotes:

```bash
# Add GitLab as origin
git remote add origin git@gitlab.spectrumflow.net:username/repo-name.git
```
```bash
# Add the bare repo on production server as prod
git remote add prod //VM0PWNEROPA6001/GIT_Repos/your-project-name.git
```
```bash
# Verify setup
git remote -v
```

## 3. Feature Development & Lifecycle Workflow
Follow this exact sequence to isolate work, track updates, and prevent breaking production.

### Step 3a: Branching & Feature Isolation
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

### Step 3b: Staging & Granular Commits
Group related changes into logical, micro-commits rather than giant, single saves.

```bash
# Check exactly what changed in the workspace
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

### Step 3c: Merging & Resolving Conflicts
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

## 4. Multi-Remote Deployment Execution
Follow this dual-push pipeline to ensure GitLab holds the definitive history before production runs the live code.

```bash
# Step 1: Push your updated main branch to GitLab (Origin)
git checkout main
git push origin main
```
* **Note:** Pushing to GitLab saves the codebase backup, logs history, and shares updates with your team.

```bash
# Step 2: Deploy verified code to your production server (Prod)
git push prod main
```
* **Note:** Pushing to `prod` triggers the server-side `post-receive` script automatically. This updates the live directory immediately.
* **Safety Warning:** Never force push (`git push -f`) to the `prod` remote. Force pushing rewritten history can break files on the live server.
