# uv Cheat Sheet: Python Packaging & Project Management

### 1. Project Management
`uv` replaces `pip`, `poetry`, and `pyenv` with a single fast tool.

```bash
# Initialize a new project
uv init my-project            # Creates pyproject.toml and basic structure
cd my-project

# Add and remove dependencies
uv add requests               # Adds to [project.dependencies] and installs
uv add --dev pytest           # Adds to [tool.uv.dev-dependencies]
uv remove requests            # Removes dependency and updates lockfile

# Synchronize the environment
uv sync                       # Installs all deps and updates uv.lock
```

---

### 2. Running Scripts & Commands
Execute code in managed environments without manual activation.

```bash
# Run a script with project dependencies
uv run main.py

# Run a command inside the virtual environment
uv run -- python --version

# Run a script with temporary dependencies (no project needed)
uv run --with requests --with pandas script.py

# Run a tool from PyPI without installing it
uvx ruff check .              # Executes 'ruff' in a temporary environment
```

---

### 3. Python Version Management
`uv` automatically downloads and manages Python versions.

```bash
# List available and installed Python versions
uv python list

# Install a specific version
uv python install 3.12

# Pin the current project to a version
uv python pin 3.11            # Creates .python-version file
```

---

### 4. Tool Management (`pipx` replacement)
Install and manage global CLI tools.

```bash
# Install a tool globally
uv tool install ruff

# List installed tools
uv tool list

# Upgrade a tool or all tools
uv tool upgrade ruff
uv tool upgrade --all

# Uninstall a tool
uv tool uninstall ruff
```

---

### 5. `pip` Compatible Interface
For those who prefer the familiar `pip` syntax with 10-100x speed.

```bash
# Basic package management
uv pip install -r requirements.txt
uv pip install flask
uv pip freeze > requirements.txt

# Inspecting environment
uv pip list                   # List installed packages
uv pip tree                   # View dependency tree
uv pip show requests          # Show package details
```

---

### 6. Maintenance & Cache
```bash
# View and clean the global cache
uv cache dir                  # Show cache location
uv cache prune                # Remove unused cache entries
uv cache clean                # Clear entire cache
```
