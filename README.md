# pve-windows-user-manager
tar -xzf pve-windows-user-manager-1.1.1.tar.gz
cd pve-windows-user-manager-1.1.1

chmod +x *.sh *.py

./install.sh

Windows User Manager for Proxmox VE

Windows User Manager is a Proxmox VE module for managing local Windows user accounts directly from the virtual machine interface.

The module operates exclusively through the QEMU Guest Agent. It does not require WinRM, SSH, additional network ports, or a separate management agent inside the Windows VM.

Features
View all local Windows users
Create new local users
Set a password during user creation
Change an existing user's password
Enable or disable local user accounts
Edit the user's full name
Edit the Windows user Description field
View all local groups available on the selected VM
Add users to one or multiple local groups
Remove users from local groups
Display current group membership for every user
Refresh users and groups directly from the Windows VM
Localized Windows support

The module does not use hardcoded group names such as:

Administrators
Users
Remote Desktop Users

Instead, the local group list is retrieved directly from the selected Windows VM.

This provides full support for localized Windows installations, including:

Administrators
Администраторы
Адміністратори
Пользователи удаленного рабочего стола
and custom groups with Cyrillic or other Unicode characters.

UTF-8 is used for user names, full names, descriptions, and group names.

VM-level management

Windows User Manager is available directly inside each QEMU virtual machine:

Virtual Machine → Windows Users

The module always works with the currently selected VM. Users and groups from different virtual machines are never mixed.

Communication architecture
Proxmox VE Web Interface
        ↓
Proxmox VE API
        ↓
QEMU Guest Agent
        ↓
PowerShell / Windows Local Accounts
        ↓
Local Windows Users and Groups
No direct network connection from Proxmox to Windows is required.

Requirements
Proxmox VE
QEMU virtual machine running Windows
QEMU Guest Agent installed inside Windows
QEMU Guest Agent enabled in the VM configuration
QEMU Guest Agent service running inside Windows
Security

All Windows management commands are executed through the existing Proxmox QEMU Guest Agent channel.

The module does not:

open additional TCP or UDP ports
enable WinRM
enable SSH
install a standalone remote administration service
store Windows administrator credentials for remote network access
Supported operations
List users
Create user
Change password
Enable user
Disable user
Edit full name
Edit description
List local groups
View group membership
Add user to group
Remove user from group
Refresh users and groups
Compatibility

The module is designed for integration with multiple Proxmox VE versions and uses the native Proxmox QEMU Guest Agent API.

Windows-side operations are designed to support both English and localized Windows installations, including systems that use Cyrillic user and group names.
