# Stage 6: Security and Troubleshooting

## Topics Covered
- Log analysis with journalctl and auth.log
- Understanding PAM authentication logging
- Sudo session tracking
- AppArmor status checking

## Commands Practiced

| Command | What it does |
|---|---|
| `journalctl -u <service> --since "1 hour ago"` | View recent logs for a specific service |
| `sudo grep "Failed password" /var/log/auth.log` | Search auth log for failed login attempts |
| `sudo grep "sudo:" /var/log/auth.log \| tail -20` | View recent sudo activity |
| `sudo aa-status` | Check AppArmor (Ubuntu's security module) status |

## Key Concepts
- **PAM** (Pluggable Authentication Modules) handles the actual authentication process behind sudo/login — its logs (`pam_unix(sudo:auth)`) show conversation failures and identity checks separately from sudo's own attempt counter
- **sudo logs the exact command attempted**, even on failure — critical for security auditing, since it ties a failed/successful auth event to a specific action
- **Every sudo command opens and closes a session** — `session opened for user root(uid=0) by (uid=1000)` immediately followed by `session closed` — this is sudo temporarily elevating privilege for one command only, not a persistent root login
- `aa-status` showing "module loaded" but "filesystem not mounted" is a **WSL-specific limitation**, not a misconfiguration — AppArmor doesn't fully activate in most WSL environments the way it would on bare-metal/VM Ubuntu

## Mini-Project: Real Incident Reconstruction from Logs

Used `/var/log/auth.log` to reconstruct my own recent command history purely from log entries — without relying on shell history:
