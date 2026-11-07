# Ashley's WSL2 Linux Dotfiles

A structured, reproducible shell and developer environment for AI Platform Engineering, managed with [chezmoi](https://www.chezmoi.io/).

---

## 1. System Environment

- **Operating System**: Ubuntu on WSL2 (Windows Subsystem for Linux)
- **Shell**: Bash (`/bin/bash`)
- **Configuration Manager**: `chezmoi`
- **Target Filesystem**: Native Linux home directory (`~/projects/`)

---

## 2. Managed Configurations

### Default Terminal Editor
Predictable terminal editor configuration to ensure interactive CLI sessions (e.g. `git commit`, `crontab -e`, `visudo`) never hang or launch unfamiliar interfaces:
- `EDITOR="nano"` and `VISUAL="nano"` exported in `~/.bashrc`
- `core.editor = nano` configured globally in `~/.gitconfig`

### Informative Shell Prompt (`PS1`)
Engineered for platform context and binary outcome observability before running critical commands:
- **User and Host (`\u@\h`)**: Clear identity indicator across local and remote environments.
- **Directory Path (`\w`)**: Full path within the Linux filesystem.
- **Git Branch Context (`parse_git_status`)**: Real-time display of the active Git branch with dirty state indicator (`*`) when uncommitted changes exist.
- **Exit Code Telemetry (`prompt_exit_code`)**: Visual red error code (`[$?]`) displayed immediately when a command exits non-zero, reinforcing binary outcome verification.

### Git Configuration
Standardised developer configuration including:
- Commit authorship name and email
- Default initialisation branch: `main`
- Line-ending normalisation (`core.autocrlf = input`)
- GitHub CLI credential helper integration

---

## 3. Installation & Usage via Chezmoi

### Initialise on a New Machine
To apply these configurations to a fresh WSL2 Ubuntu installation:

```bash
# 1. Install chezmoi
sh -c "$(curl -fsLS get.chezmoi.io)" -- -b "$HOME/.local/bin"

# 2. Initialise and apply configuration from this repository
chezmoi init --apply https://github.com/tphamthienan04/dotfiles.git

# 3. Reload shell
source ~/.bashrc
```

### Daily Workflow

```bash
# Inspect pending differences between home directory and chezmoi source
chezmoi diff

# Pull and apply latest updates from GitHub
chezmoi update

# Edit tracked configuration directly
chezmoi edit ~/.bashrc

# Sync changes made directly to ~/.bashrc or ~/.gitconfig back to chezmoi
chezmoi re-add
```

