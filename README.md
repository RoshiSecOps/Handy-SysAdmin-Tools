# Linux SysAdmin Toolbox Script

A menu-driven bash tool for practicing simple user management, system monitoring and security auditing.

- **Tech:** bash, apt, binaries required as per operation...
- **Features:** User management, system monitoring, server setup, security checks, logging

---

## 1. Project Overview

This project consists of:
- `main` - main menu an entry point to the script
- `lib/` - Directory with all additional modules.
	- `lib/user-menu` - User and Group management module.
	- `lib/server-setup-menu` - Package management module, allows for bulk installation of packages via a file.
	- `lib/system-monitoring-menu` - Basic system health information module.
	- `lib/security-audit-menu` - Security check and advisory module.
	- `lib/script-logging-function` - Functionality for logging of important actions.
	- `lib/script-init-output`- Host and User information provided at start of the script.
 
 Goal: Practice shell scripting to better understand it and later use it at work for simple tasks, CI/CD pipeline work and occasional work with Linux machines.

---

## 2. Architecture

### 2.1 Script Structure

- **Main menu:** calls into module‑specific menus:
  - User Management
  - System Monitoring
  - Server Setup
  - Security Posture

- **Logging:**
  - All important actions log to `/var/log/admin_tool.log` with level and timestamp.

---

## 3. Features

### 3.1 User Management

- Create user (with password prompt + confirmation, home dir, shell).
- Show user info:
  - username, UID, GID, shell (skipping `root`).
- Delete user (with safety checks).
- Add user to group (with validation against `/etc/group`).

### 3.2 System Monitoring

- System Info:
  - Uptime / load
  - CPU / RAM
  - OS / Kernel Info
- Currently Running Processes
  - By CPU
  - By Memory

### 3.3 Server Setup

- List default tools to install (e.g. git, curl, htop, jq, etc.).
- Bulk install tools with apt and track success/failure.
- Report which tools installed successfully and which failed.

### 3.4 Security Posture

Read‑only checks for:

- **SSH config** (`/etc/ssh/sshd_config`):
  - `PermitRootLogin`, `PasswordAuthentication`, `PermitEmptyPasswords`, etc.
- **Password policy**:
  - `/etc/login.defs` (`PASS_MAX_DAYS`, `PASS_MIN_DAYS`, `PASS_WARN_AGE`)
- **PAM password settings** (e.g. `/etc/pam.d/common-password` on Ubuntu) – presence of `pam_pwquality` / similar.
- **sudoers** (`/etc/sudoers` and `/etc/sudoers.d`):
  - Highlight risky `NOPASSWD: ALL` patterns.

Each check prints a short “OK / WARN” message; no automatic edits.

---

## 4. Usage

### 4.1 Requirements

- Ubuntu (tested on: 20.04 / 22.04 – adjust to what you actually used)
- Bash
- `sudo` privileges (for user management, installs, and some checks)

### 4.2 Running the tool

```bash
git clone https://github.com/RoshiSecOps/Handy-SysAdmin-Tools
cd Handy-SysAdmin-Tools
chmod +x main
sudo ./main
```

---

## 5. Implementation Notes

- Split into multiple modules under `lib/` for readability.
- Uses:
  - `/etc/passwd`, `/etc/group` for user and group information.
  - Standard tools: `ps`, `top`, `df`, `grep`, `cut`, `awk`, `apt-get`.
  - `systemctl` and `journalctl` for managing and inspecting services (where applicable).
- Logging:
  - Implemented via a small `log` function that writes to `/var/log/admin_tool.log`.
  - Format: `YYYY-MM-DD HH:MM:SS [LEVEL] message`.

---

## 6. Possible Future Improvements

- Add more security checks:
  - Firewall configuration (e.g., `ufw`, `iptables`).
  - World-writable files in sensitive directories.
  - SSH authorized keys permissions.
- Improve reporting:
  - Export summaries to a separate report file (e.g., JSON or CSV).
  - Add colored terminal output for OK/WARN/FAIL statuses.
- Add basic automated tests (e.g. with `shellcheck` and `bats`).
- Containerize the tool to run it in a consistent environment.
