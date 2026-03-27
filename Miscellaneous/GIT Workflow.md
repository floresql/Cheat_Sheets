# GIT Overview

Git is used for version control, and it's also a powerful tool for collaborative software development. Its  
distributed architecture allows multiple people to work on a project simultaneously without overwriting each  
other's changes.

## Key functions of Git
*   **Tracks changes to files:** Git records every modification made to a project's files over time. It  
essentially creates "snapshots" of your project at different points in its development.
*   **Allows reversion to previous versions:** If a change introduces a bug or breaks something, Git lets you  
easily go back to a previous, working version of your project.
*   **Facilitates branching and merging:** Developers can create independent copies of the codebase, called  
"branches," to work on new features or bug fixes. When the work is complete, Git can merge those changes back  
into the main branch.
*   **Creates a complete project history:** Git maintains a full timeline of all changes, which shows what was  
changed, who made the changes, and when they were made.
*   **Enables distributed development:** As a distributed version control system (DVCS), Git provides every  
developer with a full copy of the project's history. This allows them to work offline and provides a robust backup  
system, as every local copy is a complete repository.
*   **Integrates with online platforms:** When used with hosting services like GitHub, GitLab, and Bitbucket, Git  
enables developers to share code, review changes, and manage projects from anywhere in the world.

## Workflow Summary

This GitLab Flow inspired workflow uses dedicated branches for development, testing, and production to maintain  
stability and prevent accidental changes.

### Phase 1: Feature Development
1.  **Branch off `develop`**: To start a new feature, a developer creates a new, descriptively named branch  
(e.g., `feature/add-login-button`) from the  latest `develop` branch. This practice isolates ongoing work  
from the main codebase.
2.  **Commit frequently**: As they work, developers make small, frequent commits to their feature branch. Using  
a conventional commit style (e.g., `feat:`, `fix:`) helps document the type of change.
3.  **Push the feature branch**: Once ready for review, the developer pushes their feature branch to the remote  
repository.

### Phase 2: Staging and UAT Deployment
1.  **Merge to `develop`**: A developer manually merges the completed feature branch into the `develop` branch.  
This stage is suitable for code reviews.
2.  **Merge to `main`**: When a set of features is ready for testing, the `develop` branch is merged into the  
`main` branch.
3.  **Automated UAT Deployment**: Merging into `main` triggers a `post-receive` Git hook on the server, which  
automatically deploys the code to the User Acceptance Testing (UAT) environment.

### Phase 3: Production Deployment and Cleanup
1.  **Manual Production Deployment**: A PowerShell script is used for production deployment. This manual step  
requires confirmation, providing a final safety check before pushing code live.
2.  **Post-Deployment Cleanup**: After a successful production deployment, the temporary feature branches should  
be deleted both locally and on the remote repository to keep the branch history clean.

## GIT Tips

### General
- Keep branches short-lived and focused on a single feature or fix.  
- Use descriptive branch names like `feature/user-login` or `fix/billing-error`.  
- Pull changes frequently to reduce merge conflicts.  
- Always review and test before merging into `main`.  


### Commits
- `feat:` add login page validation  
- `fix:` resolve logout issue  
- `docs:` update setup instructions  
- `refactor:` simplify API endpoints  
- `test:` add unit tests for login flow  
- `chore:` update dependencies  

### GIT Command Reference

| Command | Description |
|:--|:--|
| `git fetch` | Downloads objects and refs from remote. |
| `git pull` | Fetches and merges from remote branch. |
| `git switch branch` | Switches to a branch. |
| `git switch -c name` | Creates and switches to a new branch. |
| `git status` | Shows current changes and staging state. |
| `git add .` | Stages all modified files. |
| `git commit -m "message"` | Commits staged changes. |
| `git push -u origin branch` | Pushes branch and sets upstream tracking. |
| `git merge branch` | Merges another branch into current. |
| `git branch -d branch` | Deletes a local branch. |
| `git push origin --delete branch` | Deletes a remote branch. |

---

</br></br></br>

# Git Workflow: Full Details

A lightweight, environment-based workflow inspired by **GitLab Flow**.  
This guide defines how our team collaborates, develops, tests, and deploys code using a shared Git repository.

---

## 🔑 Key Concepts

- **`develop` branch** – main branch for active feature development.  
- **`main` branch** – stable branch for UAT and production-ready code.  
- **Automatic UAT deployment** – triggered when merging into `main`.  
- **Manual production deployment** – performed directly from the production server.

---

## ⚙️ 1. Initial Setup

### Step 1: Create a Bare Central Repository (Server)

A *bare repository* stores Git history and serves as the central hub for collaboration.

```sh
# On the server
***Make sure you're using UNC Path***
cd /path/to/git-repos
mkdir project-name.git
cd project-name.git
git init --bare --shared
git branch -m main

```

---

### Step 2: Initialize Local Repositories

**Developer 1 (creates project):**

```sh
# Add the shared repo to the safe list
git config --global --add safe.directory //vm0pwneropa6001/Git_Repos/New_Repo.git

# Clone and initialize
git clone //vm0pwneropa6001/Git_Repos/New_Repo.git
cd New_Repo.git
uv init --package #to quickly scaffold a modern project with a high-performance environment.

# Create initial commit
git add .
git commit -m "Initial project setup"
git push origin main
git branch -m dev
```

**Developer 2 (joins project):**

```sh
git clone //vm0pwneropa6001/Git_Repos/New_Repo.git
cd New_Repo.git
```

---

## 🧩 2. Feature Development

### Step 1: Start a New Feature

Always branch from the latest `develop` branch.

```sh
git fetch origin
git switch develop
git pull origin develop
git switch -c feature/my-new-feature
```

---

### Step 2: Develop and Commit

Make frequent, descriptive commits using the  
**[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)** standard.

```sh
git status
git add .
git commit -m "feat: implement user authentication"
```

**Examples:**

- `feat:` add login page validation  
- `fix:` resolve logout issue  
- `docs:` update setup instructions  
- `refactor:` simplify API endpoints  
- `test:` add unit tests for login flow  
- `chore:` update dependencies  

---

### Step 3: Push Your Feature Branch

```sh
git push -u origin feature/my-new-feature
```

---

## 🧪 3. Merge & UAT Deployment

### Step 1: Merge Feature into Develop

All merges are handled manually and communicated among developers.

```sh
git fetch origin
git switch develop
git pull origin develop
git merge feature/my-new-feature
git push origin develop
```

After merge, test locally or in a dev environment.

---

### Step 2: Configure Automatic UAT Deployment (One-Time Setup)

On the **server**, configure a post-receive hook to automatically deploy when `main` is updated.

```sh
cd /path/to/git-repos/project-name.git/hooks
touch post-receive
chmod +x post-receive
```

**`post-receive` contents:**

```bash
#!/bin/bash
TARGET="//vm0pwneropa6001/Routines/Reports_UAT/New_Repo"
GIT_DIR="//vm0pwneropa6001/Routines/Git_Repos/New_Repo"
BRANCH="main"

while read oldrev newrev ref
do
  if [ "$ref" = "refs/heads/$BRANCH" ]; then
    echo "Deploying ${BRANCH} branch to UAT..."
    git --work-tree="${TARGET}" --git-dir="${GIT_DIR}" checkout -f ${BRANCH}
  else
    echo "Skipping ${ref} — only ${BRANCH} triggers UAT deployment."
  fi
done
```

---

### Step 3: Deploy to UAT

⚠️ **This step triggers the automatic UAT deployment hook.**

```sh
git switch main
git merge develop
git push origin main
```

---

## 🌍 4. Deploy to Production

Once UAT testing is complete, production deployment is **manual**. The process uses a PowerShell script to safely  
deploy project files from the User Acceptance Testing (UAT) environment to the Production environment. The script  
includes a backup step and a confirmation dialog to prevent accidental data loss.

## How to Deploy

1. Open the PowerShell `Push2Prod.ps1` script in `\\vm0pwneropa6001\Routines\Reports\`.
2. Run the script. This will launch a graphical user interface (GUI) window.
3. Select the desired project folder from the dropdown menu in the GUI.
4. Click the **Deploy to Production** button.
5. Confirm the deployment when prompted by the warning message.

## The Script Performs the Following Actions:

- **Backup**: Creates a backup of the current production folder in `\\vm0pwneropa6001\Routines\Reports\.backup\`.
- **Mirror**: Copies the contents from the UAT folder to the Production folder, mirroring the directory structure.
- **Log**: Creates a log file (`.log`) to record the process in `\\vm0pwneropa6001\Routines\Reports\.backup\` .

A "**Success**" message will appear when the deployment is complete.

### Cleanup

After deployment, delete obsolete feature branches.

```sh
git branch -d feature/my-new-feature
git push origin --delete feature/my-new-feature
```

---
