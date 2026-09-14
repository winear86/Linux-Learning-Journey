# Stage 4: Networking and Services

## Topics Covered
- Checking network interfaces and IP addresses
- Listening ports and services (ss)
- systemd service management
- Installing and testing SSH
- Basic firewall configuration (ufw)

## Commands Practiced

| Command | What it does |
|---|---|
| `ip a` | Show network interfaces and IP addresses |
| `hostname -I` | Quick view of assigned IP address(es) |
| `sudo ss -tulnp` | Show listening ports and the process using each |
| `systemctl status <service>` | Check a service's current state |
| `sudo systemctl enable --now <service>` | Enable on boot AND start immediately |
| `sudo apt install openssh-server` | Install SSH server |
| `ssh user@host` | Connect to a remote (or local) machine via SSH |
| `sudo apt install ufw` | Install the Uncomplicated Firewall |
| `sudo ufw allow ssh` | Allow SSH traffic (port 22) through the firewall |
| `sudo ufw enable` | Turn on the firewall |
| `sudo ufw status` | View current firewall rules and state |

## Key Concepts
- `ss` is the modern replacement for the older `netstat` (not installed by default on current Ubuntu)
- systemd manages services; `enable --now` is a shortcut for enabling on boot + starting immediately in one command
- SSH host keys (RSA, ECDSA, ED25519) are generated on first install — they cryptographically identify the server to clients
- **Critical safe practice:** always `ufw allow ssh` *before* `ufw enable` — otherwise you can lock yourself out of a remote server, since UFW's default policy denies all incoming traffic

## Mini-Project: Install, Enable, and Test SSH + Firewall

```bash
sudo apt install openssh-server
sudo systemctl enable --now ssh
sudo ss -tulnp | grep ssh
# tcp LISTEN 0.0.0.0:22 and [::]:22 confirmed

ssh blex@localhost
whoami   # blex — confirms real SSH session
exit     # Connection to localhost closed

sudo apt install ufw
sudo ufw allow ssh      # allow BEFORE enabling
sudo ufw enable
sudo ufw status
# Status: active
# 22/tcp ALLOW Anywhere
```

**Lesson learned:** got real end-to-end confirmation that a service can be installed, enabled, tested via live connection, and secured with a minimal firewall policy — the same sequence used to secure a real Linux server.

## Checkpoint
- [x] Can check network interfaces and listening ports
- [x] Can manage services with systemctl
- [x] Installed and tested SSH end-to-end
- [x] Configured a basic firewall policy safely
