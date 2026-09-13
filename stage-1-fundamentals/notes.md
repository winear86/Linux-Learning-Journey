# Stage 1: Linux Fundamentals

## Topics Covered
- Navigating the filesystem (absolute vs relative paths)
- Core commands: `pwd`, `ls`, `cd`
- Reading `ls -la` output (permissions, owner, size, hidden files)
- Troubleshooting "No such file or directory" errors

## Commands Practiced

| Command | What it does |
|---|---|
| `pwd` | Print current working directory |
| `ls` | List contents of current directory |
| `ls -la` | List all contents (including hidden files) with details (permissions, owner, size, date) |
| `cd /path` | Change directory using an absolute path (starts from root `/`) |
| `cd path` | Change directory using a relative path (from current location) |
| `cd ..` | Move up one directory level |
| `cd ~` | Go to home directory |
| `cd -` | Go to the previous directory |
| `hostname` | Print the machine's hostname (not a username or path) |

## Key Concepts
- **Absolute path**: starts with `/`, works from anywhere (e.g. `/home/blex/practice`)
- **Relative path**: no leading `/`, resolves from your current directory (`pwd`)
- `hostname` ≠ username — easy to confuse when reading a prompt like `user@hostname:~$`
- Always run `ls` before `cd` into an unfamiliar path — confirms the directory actually exists before you try to enter it

## Mini-Project: Real Troubleshooting Example

Attempted to `cd` into a `documents` folder that didn't exist:

```bash
cd /home/blex/documents
# -bash: cd: /home/blex/documents: No such file or directory
```

Ran `ls -la` on home directory and found the only folder present was `practice`, not `documents`. Also mistakenly tried using the machine's `hostname` as part of a path (`/home/Xjavier/documents`) — confirmed via `hostname` command that this was the machine name, not a valid user directory.

**Fix:**
```bash
cd /home/blex/practice
pwd        # confirmed: /home/blex/practice
cd ..
pwd        # confirmed: back to /home/blex
```

**Lesson learned:** don't guess folder names — verify with `ls` first. Also confirmed that `cd` requires a space before the path (`cd /path`, not `cd/path`), otherwise bash treats it as one invalid command.

## Checkpoint
- [x] Can navigate the filesystem using `pwd`, `ls`, `cd`
- [x] Understand absolute vs relative paths
- [x] Can diagnose and fix a basic "No such file or directory" error
