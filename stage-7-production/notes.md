# Stage 7: Production Linux Administration

## Topics Covered
- System monitoring basics
- Automating tasks with cron
- Full backup and restore cycle verification

## Commands Practiced

| Command | What it does |
|---|---|
| `uptime` | Show system uptime and load average |
| `df -h` | Show disk usage by filesystem, human-readable |
| `free -h` | Show memory usage, human-readable |
| `crontab -e` | Edit your personal scheduled cron jobs |
| `crontab -l` | List current cron jobs |
| `tar -xzf archive.tar.gz -C dir` | Extract a compressed archive into a target directory |

## Key Concepts
- **Cron syntax**: `minute hour day month weekday command` — `*` means "any". `0 2 * * *` = every day at 2:00 AM.
- **tar preserves full path structure** at backup time — since the original backup command referenced `$HOME/practice` (an absolute path), restoring the archive recreates that same nested path (`home/blex/practice/...`) inside the target directory, rather than dropping files directly into it.
- A backup is only proven working once you've actually **restored and verified** the files — creating the
Verified with `crontab -l` — job saved and active, will run automatically every day at 2 AM without manual intervention.

**2. Performed a full restore test:**
```bash
mkdir ~/restore_test
tar -xzf ~/backups/practice_backup_*.tar.gz -C ~/restore_test
ls -la ~/restore_test/home/blex/practice
```
Confirmed all original files restored intact (backup.sh, test.sh, notes, project folders) with correct permissions and sizes.

**Lesson learned:** completed the full production backup lifecycle — automated scheduling (cron) plus restore verification — the same pattern used in real DC/server environments to protect against data loss. A backup that's never been restore-tested is an unverified assumption, not a guarantee.

## Checkpoint
- [x] Can check system resource usage (uptime, disk, memory)
- [x] Can schedule recurring tasks with cron
- [x] Automated the Stage 5 backup script to run daily
- [x] Verified backup integrity via a full restore test
