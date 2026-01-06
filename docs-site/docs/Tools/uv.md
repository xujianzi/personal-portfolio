---
tags:
  - uv
  - python
  - tutorial
---

# UV (Astral) - Modern Python Package and Project Management

## 1. Overview

!!! note
    This guide covers essential `uv` workflows including dependency management, Python version control, and project initialization. It assumes you have basic Python knowledge.

!!! abstract
    [UV](https://astral.sh) is an extremely fast Python package and project manager written in Rust by Astral. It serves as a drop-in replacement for `pip`, `pip-tools`, `virtualenv`, and even `pyenv`. UV dramatically improves performance (10-100x faster than pip) while maintaining compatibility with existing Python packaging standards like `requirements.txt` and `pyproject.toml`.

Official Documentation: [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/)

This document provides a comprehensive guide to UV fundamentals, covering dependency management, Python version management, and modern project workflows.

**Key Features:**
- ⚡ **10-100x faster** than pip
- 🐍 Built-in Python version management
- 📦 Modern `pyproject.toml` support
- 🔒 Deterministic dependency resolution

---

## 2. Core Concepts

* **Virtual Environment**: Isolated Python environment with its own packages and dependencies
* **requirements.in**: Human-readable file listing direct dependencies
* **requirements.txt**: Machine-generated lockfile with exact versions of all dependencies
* **pyproject.toml**: Modern Python project configuration file (PEP 621 standard)
* **Python Version Management**: UV can install and manage multiple Python versions
* **UV Lock**: Deterministic dependency resolution with `uv.lock` file

---

## 3. Installation

### Install UV

```bash
# Windows (PowerShell)
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Alternative: Using pip/pipx
pipx install uv
# or
pip install uv
```

### Verify Installation

```bash
uv --version                # Display UV version
uv --help                   # Show help information
```

---

## 4. Python Version Management

!!! tip
    UV can download and manage Python versions automatically, eliminating the need for `pyenv` or manual Python installations.

### List Available Python Versions

```bash
uv python list              # List all available Python versions
uv python list --all-versions  # Include older versions
```

### Install Python Versions

```bash
uv python install 3.12      # Install latest Python 3.12.x
uv python install 3.11.8    # Install specific version
uv python install 3.12 3.11 3.10  # Install multiple versions
```

### List Installed Python Versions

```bash
uv python list --only-installed  # Show installed Python versions
```

### Pin Python Version for Project

```bash
uv python pin 3.12          # Create .python-version file
uv python pin 3.11.8        # Pin to specific version
```

!!! note
    The `.python-version` file tells UV which Python version to use for the project. This ensures consistency across team members.

### Check Current Python Version

```bash
uv python find              # Show Python version UV will use
uv run python --version     # Check Python version in UV environment
```

### Create Virtual Environment with Specific Python

```bash
uv venv --python 3.12       # Create venv with Python 3.12
uv venv --python 3.11.8     # Create venv with Python 3.11.8
uv venv --python python3.12 # Use system Python 3.12
```
### Lock Python Version for Project

```bash
uv python pin 3.12          # Lock project to Python 3.12
uv python pin 3.11.8        # Lock project to Python 3.11.8
```

---

## 5. Project Initialization and Management

### Initialize New Project with pyproject.toml

!!! tip
    Modern Python projects use `pyproject.toml` instead of `setup.py` or `requirements.txt`. UV makes it easy to initialize and manage such projects.

```bash
uv init                     # Initialize new project
uv init --name myproject    # Initialize with custom name
uv init --lib               # Initialize as a library (with src/ layout)
```

This creates:
- `pyproject.toml` - Project configuration and dependencies
- `.python-version` - Python version pin
- `README.md` - Project documentation
- Basic project structure

new project steps:
1. Initialize project with `uv init`
2. Pin Python version with `uv python pin 3.12`
3. Install dependencies with `uv add numpy pandas`
4. Add development tools with `uv add --dev ruff pytest`
5. Sync dependencies with `uv sync`

### Understanding pyproject.toml Structure

!!! note "PEP 621 Standard"
    `pyproject.toml` follows the PEP 621 standard for Python project metadata. It consolidates project configuration, dependencies, and tool settings in a single file.

#### Complete pyproject.toml Example

```toml
[project]
# Required metadata
name = "myproject"
version = "0.1.0"
description = "A comprehensive Python project"
readme = "README.md"
requires-python = ">=3.11"
license = {text = "MIT"}
authors = [
    {name = "Your Name", email = "your.email@example.com"}
]
keywords = ["example", "tutorial", "python"]
classifiers = [
    "Development Status :: 4 - Beta",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
]

# Core dependencies
dependencies = [
    "pandas>=2.0.0",
    "numpy>=1.24.0",
    "requests>=2.31.0",
]

# Optional dependency groups
[project.optional-dependencies]
dev = [
    "pytest>=7.0.0",
    "pytest-cov>=4.0.0",
    "black>=23.0.0",
    "ruff>=0.1.0",
    "mypy>=1.0.0",
]
docs = [
    "mkdocs>=1.5.0",
    "mkdocs-material>=9.0.0",
]
test = [
    "pytest>=7.0.0",
    "pytest-asyncio>=0.21.0",
]

# Entry points for CLI commands
[project.scripts]
myapp = "myproject.cli:main"
myproject-admin = "myproject.admin:run"

# URLs for project
[project.urls]
Homepage = "https://example.com"
Documentation = "https://docs.example.com"
Repository = "https://github.com/username/myproject"
Changelog = "https://github.com/username/myproject/blob/main/CHANGELOG.md"

# Build system configuration
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

# Tool-specific configurations
[tool.uv]
dev-dependencies = [
    "ipython>=8.0.0",
]

[tool.ruff]
line-length = 88
target-version = "py311"
select = ["E", "F", "I", "N", "W"]
ignore = ["E501"]

[tool.ruff.lint]
extend-select = ["Q", "RUF100", "C90"]
mccabe.max-complexity = 14

[tool.black]
line-length = 88
target-version = ["py311", "py312"]
include = '\.pyi?$'

[tool.mypy]
python_version = "3.11"
warn_return_any = true
warn_unused_configs = true
disallow_untyped_defs = true

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
python_functions = ["test_*"]
addopts = "-v --cov=myproject --cov-report=html"

[tool.coverage.run]
source = ["myproject"]
omit = ["*/tests/*", "*/test_*.py"]
```

---

### pyproject.toml Section Breakdown

#### 1. [project] - Project Metadata

!!! important "Core Section"
    The `[project]` section contains essential project information and dependencies.

**Required Fields:**
```toml
[project]
name = "myproject"              # Package name (required)
version = "0.1.0"               # Version number (required)
```

**Recommended Fields:**
```toml
description = "Short description"
readme = "README.md"            # Can also be {file = "README.md", content-type = "text/markdown"}
requires-python = ">=3.11"      # Minimum Python version
license = {text = "MIT"}        # Or {file = "LICENSE"}
authors = [
    {name = "Name", email = "email@example.com"}
]
maintainers = [
    {name = "Maintainer", email = "maint@example.com"}
]
keywords = ["web", "api"]       # PyPI search keywords
classifiers = [                 # PyPI classifiers
    "Development Status :: 4 - Beta",
    "License :: OSI Approved :: MIT License",
]
```

**Dependencies:**
```toml
dependencies = [
    "package-name",                    # Latest version
    "package>=1.0",                    # Minimum version
    "package>=1.0,<2.0",              # Version range
    "package~=1.4.2",                 # Compatible release (~= is >=1.4.2, <1.5.0)
    "package[extra]",                 # With extras
    "package @ https://example.com",  # Direct URL
]
```

**Optional Dependencies:**
```toml
[project.optional-dependencies]
dev = ["pytest", "black"]       # Install with: uv sync --extra dev
docs = ["mkdocs", "sphinx"]     # Install with: uv sync --extra docs
all = ["pytest", "mkdocs"]      # Install with: uv sync --extra all
```

**Scripts (CLI Entry Points):**
```toml
[project.scripts]
mycommand = "mypackage.module:function"    # Creates executable command
```

Example: After installation, running `mycommand` will execute `mypackage.module.function()`

**GUI Scripts:**
```toml
[project.gui-scripts]
myapp-gui = "mypackage.gui:main"           # For GUI applications
```

---

#### 2. [build-system] - Build Configuration

!!! tip "Build Backend"
    The build system defines how your package should be built and distributed.

```toml
[build-system]
requires = ["hatchling"]        # Build dependencies
build-backend = "hatchling.build"  # Build backend to use
```

**Common Build Backends:**

| Backend | Use Case | Configuration |
|---------|----------|---------------|
| `hatchling` | Modern, fast, recommended | `requires = ["hatchling"]` |
| `setuptools` | Traditional, widely compatible | `requires = ["setuptools>=61.0"]` |
| `flit_core` | Lightweight, simple projects | `requires = ["flit_core>=3.2"]` |
| `poetry-core` | Poetry projects | `requires = ["poetry-core>=1.0.0"]` |
| `pdm-backend` | PDM projects | `requires = ["pdm-backend"]` |

**Example with Hatchling:**
```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.hatchling.build.targets.wheel]
packages = ["src/mypackage"]
```

**Example with Setuptools:**
```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[tool.setuptools.packages.find]
where = ["src"]
include = ["mypackage*"]
```

---

#### 3. [tool.*] - Tool-Specific Configurations

!!! tip "Centralized Configuration"
    The `[tool]` sections allow you to configure various development tools in a single file.

##### tool.uv - UV Configuration

```toml
[tool.uv]
dev-dependencies = [
    "ipython>=8.0.0",
    "ipdb>=0.13.0",
]

[tool.uv.sources]
# Use specific package sources
my-package = { git = "https://github.com/user/repo.git" }
another-package = { path = "../local-package", editable = true }
```

##### tool.ruff - Python Linter & Formatter

```toml
[tool.ruff]
# General settings
line-length = 88
target-version = "py311"
exclude = [
    ".git",
    ".venv",
    "__pycache__",
    "build",
    "dist",
]

# Linting rules
select = [
    "E",   # pycodestyle errors
    "F",   # pyflakes
    "I",   # isort
    "N",   # pep8-naming
    "W",   # pycodestyle warnings
]
ignore = ["E501"]  # Line too long

[tool.ruff.lint]
extend-select = ["Q", "RUF100", "C90"]
mccabe.max-complexity = 14

[tool.ruff.format]
quote-style = "double"
indent-style = "space"

[tool.ruff.lint.isort]
known-first-party = ["myproject"]
```

##### tool.black - Code Formatter

```toml
[tool.black]
line-length = 88
target-version = ["py311", "py312"]
include = '\.pyi?$'
exclude = '''
/(
    \.git
  | \.venv
  | build
  | dist
)/
'''
```

##### tool.mypy - Type Checker

```toml
[tool.mypy]
python_version = "3.11"
warn_return_any = true
warn_unused_configs = true
warn_redundant_casts = true
disallow_untyped_defs = true
disallow_any_generics = true
check_untyped_defs = true
no_implicit_reexport = true

# Per-module options
[[tool.mypy.overrides]]
module = "tests.*"
disallow_untyped_defs = false
```

##### tool.pytest - Testing Framework

```toml
[tool.pytest.ini_options]
# Test discovery
testpaths = ["tests"]
python_files = ["test_*.py", "*_test.py"]
python_functions = ["test_*"]
python_classes = ["Test*"]

# Options
addopts = [
    "-v",                           # Verbose
    "--strict-markers",             # Strict marker usage
    "--cov=myproject",              # Coverage for myproject
    "--cov-report=html",            # HTML coverage report
    "--cov-report=term-missing",    # Show missing lines
]

# Markers
markers = [
    "slow: marks tests as slow",
    "integration: marks tests as integration tests",
]
```

##### tool.coverage - Code Coverage

```toml
[tool.coverage.run]
source = ["myproject"]
omit = [
    "*/tests/*",
    "*/test_*.py",
    "*/__pycache__/*",
]
branch = true

[tool.coverage.report]
exclude_lines = [
    "pragma: no cover",
    "def __repr__",
    "raise AssertionError",
    "raise NotImplementedError",
    "if __name__ == .__main__.:",
]
```

---

### Using pyproject.toml with UV

#### Install All Dependencies

```bash
uv sync                         # Install production dependencies
uv sync --extra dev             # Install with dev dependencies
uv sync --extra dev --extra docs  # Install multiple groups
uv sync --all-extras            # Install all optional dependencies
```

#### Install Project in Editable Mode

```bash
uv pip install -e .             # Editable install (for development)
```

!!! note "Editable Install"
    Editable mode allows you to modify source code without reinstalling. Changes take effect immediately.

#### Run Tools Configured in pyproject.toml

```bash
# Run tests with pytest configuration from pyproject.toml
uv run pytest

# Format code with black configuration
uv run black .

# Lint with ruff configuration
uv run ruff check .

# Type check with mypy configuration
uv run mypy src/
```

#### Build and Publish Package

```bash
# Build package (uses build-system configuration)
uv build

# This creates:
# - dist/myproject-0.1.0.tar.gz (source distribution)
# - dist/myproject-0.1.0-py3-none-any.whl (wheel)
```

---

### Practical Example: Complete Project Setup

```bash
# 1. Initialize project
uv init myproject
cd myproject

# 2. Pin Python version
uv python pin 3.11

# 3. Add production dependencies
uv add fastapi uvicorn sqlalchemy pydantic

# 4. Add development dependencies
uv add --dev pytest pytest-cov black ruff mypy

# 5. Add documentation dependencies
uv add --dev mkdocs mkdocs-material

# 6. Sync all dependencies
uv sync --all-extras

# 7. Run your application
uv run python -m myproject
```

Your `pyproject.toml` will be automatically updated with all dependencies and ready for team collaboration!

### Add Dependencies to pyproject.toml

```bash
uv add pandas               # Add pandas to dependencies
uv add "numpy>=1.24"        # Add with version constraint
uv add --dev pytest         # Add to dev dependencies
uv add "flask[async]"       # Add with extras
```

!!! note
    `uv add` automatically updates `pyproject.toml` and installs the package.

### Remove Dependencies

```bash
uv remove pandas            # Remove package
uv remove --dev pytest      # Remove dev dependency
```

### Install Project Dependencies

```bash
uv sync                     # Install all dependencies from pyproject.toml
uv sync --dev               # Include dev dependencies
uv sync --no-dev            # Only production dependencies
```

### Using uv to install pytorch
1️⃣ 先加依赖
```bash
uv add torch torchvision torchaudio
```
2️⃣ 在 pyproject.toml 里指定 CUDA index（Linux / Windows）
```toml
[tool.uv.sources]
torch = [{ index = "pytorch-cu126" }]
torchvision = [{ index = "pytorch-cu126" }]
torchaudio = [{ index = "pytorch-cu126" }]

[[tool.uv.index]]
name = "pytorch-cu126"
url = "https://download.pytorch.org/whl/cu126"
explicit = true
```
3️⃣ 同步并锁版本
```bash
uv sync
```
Verify Installation:
```python
import torch
print(torch.cuda.is_available())
print(torch.cuda.get_device_name(0))
```

---

## 6. Traditional Workflow (requirements.txt)

!!! tip
    If you're working with existing projects that use `requirements.txt`, UV fully supports this workflow while providing faster performance.

### Step 1: Create Virtual Environment

```bash
uv venv                     # Create virtual environment
# Activate the virtual environment
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```
!!! note
    This creates a `.venv/` directory with an isolated Python environment.

### Step 2: Define Your Dependencies

Create a `requirements.in` file:

```text
dash
pandas
plotly
```
!!! important "Why we need `requirements.in`?"
    `requirements.in` is a file that contains all the dependencies of your project. It is used to specify the exact versions of the dependencies that you want to use. This is important because it ensures that the project is reproducible. If you don't specify the exact versions of the dependencies, you may get different results when running the project on different machines.
!!! tip "What is `requirements.txt`?"
    `requirements.txt` is a file that contains all the dependencies of your project. It is used to specify the exact versions of the dependencies that you want to use. This is important because it ensures that the project is reproducible. If you don't specify the exact versions of the dependencies, you may get different results when running the project on different machines.

| 对比项        | 直接写 `requirements.txt` | 写 `requirements.in` + compile |
| ---------- | ---------------------- | ----------------------------- |
| 依赖清晰性      | ❌ 差（包含过多不必要信息）         | ✅ 清晰，只写直接依赖                   |
| 可维护性       | ❌ 版本手动调整繁琐             | ✅ 自动解析、锁定版本                   |
| 可复现性       | ❌ 易受包升级影响              | ✅ 强一致性、适合部署                   |
| 团队协作       | ❌ 容易出错                 | ✅ 更安全稳定                       |
| 与 CI/CD 集成 | ⚠️ 不稳定                 | ✅ 更可靠                         |



### Step 3: Compile to Locked Requirements File

```bash
uv pip compile requirements.in -o requirements.txt
```
!!! Success "Lock exact versions"
    This resolves full dependency tree and locks exact versions.

### Step 4: Install from Locked File

```bash
uv pip install -r requirements.txt
```

This installs all dependencies into your environment based on `requirements.txt`.

### Step 5: Run Your Application

```bash
uv run python app.py        # Run Python script with UV
python app.py               # Or use activated environment directly
```

---

## 7. Development vs Production Environments

!!! tip
    Separating development tools from production dependencies keeps your deployment lean and secure, especially when deploying to Docker containers.

### `requirements.in`

```text
dash
pandas
plotly
```

### `dev-requirements.in`

```text
pytest
black
flake8
mypy
```

### Compile and Install Development Dependencies

```bash
uv pip compile dev-requirements.in -o dev-requirements.txt
uv pip install -r dev-requirements.txt
```

---

## 8. Essential Commands Reference

### Environment Management

```bash
uv venv                             # Create virtual environment
uv venv --python 3.12               # Create with specific Python version
uv venv .venv                       # Specify custom directory
```

### Package Management

```bash
uv pip install <package>            # Install single package
uv pip install -r requirements.txt  # Install from requirements file
uv pip install -e .                 # Install project in editable mode
uv pip uninstall <package>          # Uninstall package
uv pip list                         # List installed packages
uv pip freeze                       # Output installed packages
uv pip show <package>               # Show package information
```

### Dependency Compilation

```bash
uv pip compile requirements.in -o requirements.txt       # Compile requirements
uv pip compile requirements.in --upgrade                 # Upgrade all packages
uv pip compile requirements.in --upgrade-package pandas  # Upgrade specific package
uv pip sync requirements.txt                             # Sync environment to exact requirements
```

### Python Version Management

```bash
uv python list                      # List available Python versions
uv python install 3.12              # Install Python version
uv python pin 3.12                  # Pin project to Python version
uv python find                      # Show which Python will be used
```

### Project Management (pyproject.toml)

```bash
uv init                             # Initialize new project
uv add <package>                    # Add dependency
uv add --dev <package>              # Add dev dependency
uv remove <package>                 # Remove dependency
uv sync                             # Sync project dependencies
uv lock                             # Generate uv.lock file
uv run <command>                    # Run command in project environment
```

### Quick Reference Table

| Command | Description |
|---------|-------------|
| `uv venv` | Create virtual environment |
| `uv pip install` | Install packages |
| `uv pip compile` | Lock dependency versions |
| `uv pip sync` | Sync environment exactly |
| `uv python install` | Install Python version |
| `uv python pin` | Pin project Python version |
| `uv init` | Initialize new project |
| `uv add` | Add dependency to pyproject.toml |
| `uv sync` | Install project dependencies |
| `uv run` | Run command in environment |

---

## 9. Automation Scripts

### Windows Setup Script (`setup_env.bat`)

!!! tip
    This script automates the environment setup for Windows. Run this after cloning a repository to quickly set up your development environment.

```bat
@echo off
echo Creating virtual environment...
uv venv

echo Compiling production dependencies...
uv pip compile requirements.in -o requirements.txt

echo Installing production dependencies...
uv pip install -r requirements.txt

echo Compiling development dependencies...
uv pip compile dev-requirements.in -o dev-requirements.txt

echo Installing development dependencies...
uv pip install -r dev-requirements.txt

echo.
echo Environment setup complete!
echo To activate: .venv\Scripts\activate
```

### macOS/Linux Setup Script (`setup_env.sh`)

!!! tip
    Make the script executable with `chmod +x setup_env.sh` before running.

```bash
#!/bin/bash
set -e  # Exit on error

echo "Creating virtual environment..."
uv venv

echo "Compiling production dependencies..."
uv pip compile requirements.in -o requirements.txt

echo "Installing production dependencies..."
uv pip install -r requirements.txt

echo "Compiling development dependencies..."
uv pip compile dev-requirements.in -o dev-requirements.txt

echo "Installing development dependencies..."
uv pip install -r dev-requirements.txt

echo ""
echo "Environment setup complete!"
echo "To activate: source .venv/bin/activate"
```

---

## 10. Version Control Best Practices

### Recommended .gitignore

!!! note
    Choose whether to commit lockfiles (`requirements.txt`, `uv.lock`) based on your project type. For applications: commit them. For libraries: ignore them.

```gitignore
# Virtual environment
.venv/
venv/
env/

# Python cache
__pycache__/
*.py[cod]
*.pyo
*.pyd
*.so
.Python

# Distribution / packaging
build/
dist/
*.egg-info/
.eggs/

# UV cache
.uv/

# Logs and local config
*.log
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db

# Lockfiles (uncomment if you want to ignore them)
# requirements.txt
# dev-requirements.txt
# uv.lock
```

!!! tip "For Team Projects"
    **Do commit** `requirements.txt`, `dev-requirements.txt`, and `uv.lock` to ensure all team members use identical dependency versions. **Do ignore** `.venv/` and cache directories.

---

## 11. Common Workflows

### Starting a New Project with pyproject.toml

```bash
# 1. Initialize project
uv init myproject
cd myproject

# 2. Pin Python version
uv python pin 3.12

# 3. Add dependencies
uv add pandas numpy plotly

# 4. Add dev dependencies
uv add --dev pytest black ruff

# 5. Sync environment
uv sync

# 6. Run your application
uv run python main.py
```

### Working with Existing Project (requirements.txt)

```bash
# 1. Clone repository
git clone <repository-url>
cd project

# 2. Create virtual environment with specific Python
uv venv --python 3.11

# 3. Activate environment
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

# 4. Install dependencies
uv pip install -r requirements.txt

# 5. Run application
python app.py
```

### Migrating from pip to UV

```bash
# 1. Install UV
pipx install uv

# 2. Create requirements.in from existing requirements.txt
# (manually extract only direct dependencies)

# 3. Compile with UV
uv pip compile requirements.in -o requirements.txt

# 4. Create new environment
uv venv

# 5. Install with UV
uv pip install -r requirements.txt
```

---

## 12. Best Practices

!!! tip "Recommended Practices"
    - **Use pyproject.toml** for new projects instead of requirements.txt
    - **Pin Python versions** with `.python-version` for consistency
    - **Separate dev dependencies** from production dependencies
    - **Commit lockfiles** for applications, ignore for libraries
    - **Use `uv sync`** instead of manual installs for reproducible environments
    - **Leverage `uv run`** to avoid manual environment activation

### Why Use pyproject.toml?

| Feature | requirements.txt | pyproject.toml |
|---------|------------------|----------------|
| Dependency groups | Manual files | Built-in (dev, optional) |
| Metadata | Separate files | Single file |
| Modern standard | No | Yes (PEP 621) |
| Tool configuration | Separate files | Single file |
| Build system | No | Yes |

---

## 13. Troubleshooting

### UV command not found

```bash
# Reinstall UV
curl -LsSf https://astral.sh/uv/install.sh | sh
# Add to PATH (Linux/macOS)
export PATH="$HOME/.cargo/bin:$PATH"
```

### Python version not found

```bash
# List available versions
uv python list

# Install specific version
uv python install 3.12

# Verify installation
uv python list --only-installed
```

### Dependency conflicts

```bash
# Show detailed resolution
uv pip compile requirements.in --verbose

# Try different resolver
uv pip compile requirements.in --resolution highest
```

### Virtual environment activation issues

**Windows PowerShell:**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
.venv\Scripts\Activate.ps1
```

**Linux/macOS:**
```bash
chmod +x .venv/bin/activate
source .venv/bin/activate
```

---

## 14. Additional Resources

!!! info "Learn More"
    - **Official Documentation:** [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/)
    - **GitHub Repository:** [https://github.com/astral-sh/uv](https://github.com/astral-sh/uv)
    - **Blog & Updates:** [https://astral.sh/blog](https://astral.sh/blog)
    - **Python Packaging Guide:** [https://packaging.python.org/](https://packaging.python.org/)

---

## 15. Summary

UV revolutionizes Python package and project management by providing:

- **Speed**: 10-100x faster than traditional tools
- **Python Version Management**: Built-in Python installation and management
- **Modern Standards**: First-class support for `pyproject.toml` (PEP 621)
- **Compatibility**: Drop-in replacement for pip, pip-tools, and virtualenv
- **Reliability**: Deterministic dependency resolution with lockfiles

Whether you're starting a new project with `pyproject.toml` or maintaining an existing one with `requirements.txt`, UV provides the performance and reliability you need for modern Python development.
