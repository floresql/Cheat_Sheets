# Git Multi-Remote Workflow Cheat Sheet (GitLab & Windows Network Prod Server)

## 1. Production Server Configuration
Set up the bare repository and deployment directory on your remote network share server via Git Bash.

## Path & Directory Configuration
***Always use forward slashes (`//`) for UNC network paths within Git Bash.***

```bash
# Create a directory for the live website files on the network share
mkdir -p //VM0PWNEROPA6001/NewDirName
```
```bash
# Navigate to the remote network share repository root
cd //VM0PWNEROPA6001/GIT_Repos

# Create the dedicated repository directory
mkdir your-project-name.git
cd your-project-name.git
```
```bash
# Initialize the bare repository with shared workgroup permissions
git init --bare --shared=all
git branch -m main
```
```bash
# Create and open the post-receive hook file
nano hooks/post-receive
```

### Post-Receive Hook Script
Paste the following exact script into the `hooks/post-receive` file. 

```bash
#!/bin/bash
# Define deployment targets using Git Bash compatible network paths
TARGET="//VM0PWNEROPA6001/NewDirName"
GIT_DIR="//VM0PWNEROPA6001/GIT_Repos/your-project-name.git"

# Unset conflicting local Git environment variables
unset GIT_INDEX_FILE

# Deploy the code to the live directory forcing the main branch layout
mkdir -p "\$TARGET"
git --work-tree="\(TARGET" --git-dir="\)GIT_DIR" checkout -f main

# Optional: Add build tasks matching your Windows/IIS server layout
# cd "\$TARGET" && npm install --production
```

Make the hook script executable:

```bash
chmod +x hooks/post-receive
```

## 2. Local Machine Authentication & Setup
Generate SSH keys locally within Git Bash and link them to GitLab for seamless authentication.

```bash
# Generate a secure modern SSH key pair
ssh-keygen -t ed25519 -C "your_email@example.com"
```
```bash
# Start the ssh-agent context inside Git Bash
eval "\$(ssh-agent -s)"
```
```bash
# Add your SSH private key to the agent
ssh-add ~/.ssh/id_ed25519
```
```bash
# Display the public key to copy/paste into GitLab Settings -> SSH Keys
cat ~/.ssh/id_ed25519.pub
```

Configure your local Git repository network remotes:

```bash
# Add GitLab as origin
git remote add origin git@gitlab.spectrumflow.net:username/repo-name.git
```
```bash
# Add the bare network share repository as the prod target
git remote add prod //VM0PWNEROPA6001/GIT_Repos/your-project-name.git
```
```bash
# Verify both transport targets are mapped correctly
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
# Step 2: Deploy verified code directly over the network to the production server (Prod)
git push prod main
```
* **Note:** Pushing to `prod` triggers the network-based `post-receive` script automatically. This updates the live directory immediately.
* **Safety Warning:** Never force push (`git push -f`) to the `prod` remote. Force pushing rewritten history can break files on the live server.
