# Stage 3: System Administration Basics

## Topics Covered
- Package management (apt)
- User and group management
- sudo access and group membership

## Commands Practiced

| Command | What it does |
|---|---|
| `sudo apt update` | Refresh list of available packages |
| `whoami` | Print current username |
| `id` | Show UID, GID, and all groups for current user |
| `groups` | List groups the current user belongs to |
| `sudo useradd -m testuser` | Create a new user with a home directory |
| `sudo passwd testuser` | Set/reset a password for a user |
| `id testuser` | Show UID/GID/groups for a specific user |
| `sudo usermod -aG sudo testuser` | Add a user to the sudo group (append, not overwrite) |

## Key Concepts
- Membership in the `sudo` group is what grants a user admin privileges on Ubuntu — visible directly in `id`/`groups` output
- `usermod -aG group user` — the `-a` (append) flag is critical; without it, `usermod` **overwrites** all existing group memberships with just the one specified
- `groups username` only works with an exact existing username — `groups test user` was read as two separate (nonexistent) usernames, not one

## Troubleshooting: Forgotten sudo Password (WSL)

Hit "sudo: 2 incorrect password attempts" when running `sudo apt update` — 
had forgotten the password set during initial WSL Ubuntu setup.

**Fix (WSL-specific):**
```powershell
# From Windows PowerShell (not inside Ubuntu):
wsl -u root
```
```bash
# Now inside Ubuntu as root:
passwd blex
exit
```
Reopened normal Ubuntu terminal, `sudo apt update` succeeded with new password.

**Lesson learned:** WSL lets you drop into any distro as root via `wsl -u root` 
from Windows — useful recovery path when locked out of sudo, since there's 
no GRUB/recovery mode like a full Linux install would need.

## Mini-Project: Create and Configure a Test User

```bash
sudo useradd -m testuser
sudo passwd testuser
id testuser
# uid=1001(testuser) gid=1001(testuser) groups=1001(testuser)

sudo usermod -aG sudo testuser
groups testuser
# testuser : testuser sudo
```

**Lesson learned:** a freshly created user starts with only their own private group; explicit `usermod -aG` calls are needed to grant additional access like sudo.

## Checkpoint
- [x] Can update package lists with apt
- [x] Understand user identity (uid/gid) and group membership
- [x] Can create a user and manage their group membership
- [x] Understand how sudo access is tied to group membership
