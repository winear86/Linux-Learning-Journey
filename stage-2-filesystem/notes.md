# Stage 2: Working with the Linux Filesystem

## Topics Covered
- File permissions (read, write, execute)
- Symbolic vs numeric chmod
- Permission structure: owner / group / others

## Commands Practiced

| Command | What it does |
|---|---|
| `touch file` | Create an empty file |
| `chmod u+x file` | Add execute permission for the owner (symbolic) |
| `chmod g+w file` | Add write permission for the group (symbolic) |
| `chmod 755 file` | Set permissions numerically (owner=rwx, group=r-x, others=r-x) |

## Key Concepts
- Permission string format: `[type][owner][group][others]`
  e.g. `-rwxr-xr-x` = regular file, owner has rwx, group has r-x, others have r-x
- **Symbolic chmod** (`u+x`, `g+w`, `o-r`) **adds/removes** a specific permission without touching the rest
- **Numeric chmod** (`755`, `644`) **sets the whole permission set at once** — overwrites previous state
  - Numeric values: `r=4, w=2, x=1` — sum per group (owner/group/others)
- `cd /practice` (absolute, from root) fails if the folder isn't actually at root — `cd practice` or `cd ~/practice` is correct if it's inside your home directory

## Mini-Project: Permission Changes on test.sh

```bash
touch test.sh
ls -la test.sh
# -rw-r--r--  (default: owner rw-, group r--, others r--)

chmod u+x test.sh
ls -la test.sh
# -rwxr--r--  (added execute for owner only)

chmod 755 test.sh
ls -la test.sh
# -rwxr-xr-x  (numeric: owner rwx, group r-x, others r-x)

chmod g+w test.sh
ls -la test.sh
# -rwxrwxr-x  (added write for group, on top of 755 state)
```

**Lesson learned:** symbolic chmod is additive/subtractive on the current permissions; numeric chmod resets the entire permission set in one command.

## Checkpoint
- [x] Understand permission structure (owner/group/others, rwx)
- [x] Can use `chmod` symbolically (`u+x`, `g+w`) and numerically (`755`)
- [x] Practiced creating a file and modifying its permissions
