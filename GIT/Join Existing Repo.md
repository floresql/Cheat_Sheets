# Joining an Existing Git Repository

Use this guide if you are onboarding to a project that has already been initialized on GitLab and the production network server.

## 1. Local Machine Authentication
Generate SSH keys locally within Git Bash and link them to GitLab for authentication.

```bash
# Generate a secure modern SSH key pair
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start the ssh-agent context inside Git Bash
eval "\$(ssh-agent -s)"

# Add your SSH private key to the agent
ssh-add ~/.ssh/id_ed25519

# Display the public key to copy/paste into GitLab Settings -> SSH Keys
cat ~/.ssh/id_ed25519.pub
```

## 2. Repository Cloning & Environment Setup
Run these commands in Git Bash to clone the repository and configure your remote paths.

*Always use forward slashes (`//`) for UNC network paths within Git Bash.*

```bash
# Clone the repository from the shared network location
git clone //vm0pwneropa6001/Git_Repos/New_Repo.git
cd New_Repo.git

# Add GitLab as origin remote
git remote add origin git@gitlab.spectrumflow.net:username/repo-name.git

# Add the bare network share repository as the prod target
git remote add prod //VM0PWNEROPA6001/GIT_Repos/your-project-name.git

# Verify both transport targets are mapped correctly
git remote -v
```
