# UV (Astral) Python Dependency Management - Usage Guide

## Overview
!!! Abstract "OverView"
    `uv` is a modern Python package management tool built by [Astral](https://astral.sh), written in Rust. It is designed to replace `pip`, `pip-tools`, and `virtualenv` with a fast, reliable, and reproducible package workflow. It dramatically improves performance and dependency resolution while remaining compatible with existing standards such as `requirements.txt` and `pyproject.toml`.

## Why Use `uv`

* Ultra-fast dependency installation
* Deterministic builds via `requirements.txt` or `lock` files
* Seamless virtual environment creation
* Drop-in replacement for pip and pip-tools
* Clear separation between development and production dependencies

## Installation

```bash
pipx install uv
# or
pip install uv
```

## Basic Workflow

### Step 1: Create Virtual Environment

```bash
uv venv
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
uv pip run python app.py
```

## Development vs Production Environments
!!! tip
    It's helpful to separate dev tools from production, espacially when deploying to docker
To separate dev tools from production:

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

Compile and install separately:

```bash
uv pip compile dev-requirements.in -o dev-requirements.txt
uv pip install -r dev-requirements.txt
```

## Common Commands

| Command              | Description                                |
| -------------------- | ------------------------------------------ |
| `uv venv`            | Create virtual environment                 |
| `uv pip install ...` | Install packages using uv engine           |
| `uv pip compile`     | Lock dependency versions                   |
| `uv pip sync`        | Sync environment to exact requirements.txt |
| `uv pip run`         | Run command inside virtual environment     |
| `uv pip list`        | Show installed packages                    |

---

## Windows Setup Script (`setup_env.bat`)
!!! tip
    This script is for Windows users. For Linux/macOS, use the provided `.sh` scripts. You can automatically run this script after cloning the repo.

```bat
@echo off
uv venv
uv pip compile requirements.in -o requirements.txt
uv pip install -r requirements.txt
uv pip compile dev-requirements.in -o dev-requirements.txt
uv pip install -r dev-requirements.txt
@echo Environment setup complete.
```

## macOS/Linux Setup Script (`setup_env.sh`)

```bash
#!/bin/bash
uv venv
uv pip compile requirements.in -o requirements.txt
uv pip install -r requirements.txt
uv pip compile dev-requirements.in -o dev-requirements.txt
uv pip install -r dev-requirements.txt
echo "Environment setup complete."
```

---

## .gitignore

```gitignore
# Virtual environment
.venv/

# Python cache
__pycache__/
*.py[cod]
*.pyo
*.pyd

# Logs and local config
*.log
.env

# OS files
.DS_Store
Thumbs.db

# Locked files (if you generate them)
requirements.txt
requirements.lock
dev-requirements.txt
```

---

For more, visit: [https://astral.sh/uv](https://astral.sh/uv)
