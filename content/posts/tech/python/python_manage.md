+++
title = 'Python Manage'
date = 2025-10-16T14:22:00+08:00
draft = false
slug = "e985480"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Python Manage

Extremely fast Python package and project manager, written in Rust.

## Highlight
- 🚀 A single tool to replace pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more.  
- ⚡️ 10-100x faster than pip.  
- 🗂️ Provides comprehensive project management, with a universal lockfile.  
- ❇️ Runs scripts, with support for inline dependency metadata.  
- 🐍 Installs and manages Python versions.  
- 🛠️ Runs and installs tools published as Python packages.  
- 🔩 Includes a pip-compatible interface for a performance boost with a familiar CLI.  
- 🏢 Supports Cargo-style workspaces for scalable projects.  
- 💾 Disk-space efficient, with a global cache for dependency deduplication.  
- ⏬ Installable without Rust or Python via curl or pip.  
- 🖥️ Supports macOS, Linux, and Windows.  

## Installation ( Windows )
Install uv with our official standalone installer:
>```powershell
> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
>```
>
Request a specific version by including it in the URL:
>```powershell
> powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/0.9.3/install.ps1 | iex"
>```
>

> [!TIP]
>
> The installation script may be inspected before use:
>
> ```powershell
> powershell -c "irm https://astral.sh/uv/install.ps1 | more"
> ```
> 


## Installation ( Linux Ubuntu )
uv provides a standalone installer to download and install uv:  
Use curl to download the script and execute it with sh:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

If your system doesn't have curl, you can use wget:
```bash
wget -qO- https://astral.sh/uv/install.sh | sh
```

Request a specific version by including it in the URL:
```bash
curl -LsSf https://astral.sh/uv/0.9.3/install.sh | sh
```

> [!TIP]
>
> The installation script may be inspected before use:
>
> ```powershell
> curl -LsSf https://astral.sh/uv/install.sh | less
> ```
> 