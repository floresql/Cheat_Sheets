# Git Multi-Remote Setup Guide (GitLab & Windows Network Prod Server)

## 1. Production Server Configuration
Set up the bare repository and deployment directory on your remote network share server via Git Bash.

### Path & Directory Configuration
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
Paste the following exact script into the `hooks/post-receive` file:

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
