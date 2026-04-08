# Python src-layout Cheat Sheet

### 1. Using `uv` (Fastest/Recommended)
# Initialize a new library project with src/ layout
uv init --lib my_project

# Structure created:
# my_project/
# ├── pyproject.toml
# └── src/
#     └── my_project/
#         ├── __init__.py
#         └── hello.py

---

### 2. Using `Poetry`
# Create a new project folder with src/ layout
poetry new --src my_project

# Structure created:
# my_project/
# ├── pyproject.toml
# ├── src/
# │   └── my_project/
# │       └── __init__.py
# └── tests/

---

### 3. Manual Terminal Setup (Universal)
# Create the directory tree
mkdir -p my_project/src/my_package
mkdir -p my_project/tests

# Create essential files
touch my_project/pyproject.toml
touch my_project/README.md
touch my_project/src/my_package/__init__.py
touch my_project/src/my_package/main.py
touch my_project/tests/test_main.py

# Final Structure:
# my_project/
# ├── pyproject.toml
# ├── README.md
# ├── src/
# │   └── my_package/
# │       ├── __init__.py
# │       └── main.py
# └── tests/
#     └── test_main.py

---

### 4. Minimal `pyproject.toml` (Setuptools)
# Add this to your pyproject.toml so your code is discoverable.

[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "my_package"
version = "0.1.0"

[tool.setuptools.packages.find]
where = ["src"]
