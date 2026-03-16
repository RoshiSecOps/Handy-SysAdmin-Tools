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

