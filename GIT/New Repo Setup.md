# Initial Git Repository Setup Guide

Use this guide to set up a new bare repository on the production network server and initialize the project locally.

## 1. Production Server Configuration

Run these commands in Git Bash to set up the bare repository and deployment directory on the remote network share.

### Path and Directory Configuration

> Always use forward slashes (`//`) for UNC network paths within Git Bash.

1. Log in to `VM0PWNEROPA6001` and go to `D:\`.
2. Create a new directory named `NewDirName`.
3. Share the new directory so it can be accessed directly via `//VM0PWNEROPA6001/NewDirName`.
4. Exit the server.

Then run:

````bash
# Navigate to the remote network share repository root in Bash
cd //VM0PWNEROPA6001/GIT_Repos

# Create the dedicated repository directory
mkdir your-project-name.git
cd your-project-name.git

# Initialize the bare repository with shared workgroup permissions
git init --bare --shared
git config --global --add safe.directory '%(prefix)///vm0pwneropa6001/d/GIT_Repos/New_Repo.git'
git branch -m main

# Create and open the post-receive hook file
nano hooks/post-receive
````

### Post-Receive Hook Script

Paste the following script into `hooks/post-receive`:

````bash
#!/usr/bin/env bash

# Define the production target folder and Git repository path
TARGET="//VM0PWNEROPA6001/NewDirName"
GIT_DIR="//VM0PWNEROPA6001/GIT_Repos/your-project-name.git"

while read oldrev newrev ref
do
    # Check if the updated reference is the main branch
    if [[ $ref = refs/heads/main ]]; then
        echo "Main branch push received. Deploying code to production..."
        
        # Force checkout the code into the targeted live working tree
        git --work-tree=$TARGET --git-dir=$GIT_DIR checkout -f
    else
        echo "Ref $ref received. No deployment actions defined for this branch."
    fi
done
````

In `nano`:

1. Press `Ctrl+O` to write the file.
2. Press `Enter` to confirm the file name.
3. Press `Ctrl+X` to exit.

Make the hook script executable:

````bash
chmod +x hooks/post-receive
````

## 2. Local Machine Authentication (First-Time GitLab Setup)

Generate SSH keys locally within Git Bash and link them to GitLab for seamless authentication.

````bash
# Generate a secure modern SSH key pair
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start the ssh-agent context inside Git Bash
eval "$(ssh-agent -s)"

# Add your SSH private key to the agent
ssh-add ~/.ssh/id_ed25519

# Display the public key to copy/paste into GitLab Settings > SSH Keys
cat ~/.ssh/id_ed25519.pub
````

## 3. Project Creation and Initialization

On your local machine, navigate to your local repo folder in Bash, for example `C:\git_local`.

````bash
# Add the shared repo to the safe list
git config --global --add safe.directory //vm0pwneropa6001/Git_Repos/New_Repo.git

# Clone and initialize
git clone //vm0pwneropa6001/Git_Repos/New_Repo.git
cd New_Repo
git remote rename origin prod

# Quickly scaffold a modern project with a high-performance environment
uv init --package

# If necessary, run this first to install uv
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
````

### Create the Project in GitLab

1. Go to your group page on GitLab: `https://gitlab.spectrumflow.net/noa`
2. Click **New project**.
3. Select **Create blank project**.
4. Set the **Project URL** dropdown to match your specific group namespace.
5. Provide a project name.
6. Uncheck **Initialize repository with a README**.
7. Click **Create project**.

Then run:

````bash
# Add GitLab as dev remote
git remote add dev git@gitlab.spectrumflow.net:noa/repo-name.git

# Create initial commit and push
git add .
git commit -m "Initial project setup"
git push --set-upstream dev main

# Verify both transport targets are mapped correctly
git remote -v

# Always push to PROD manually
git push prod main
````