# 17 – Linux Security & Hardening

## 🎯 Objectives
- Secure a Linux server using firewalls, access controls and hardening best practices

## 📘 Theory Notes
- **Hardening** = reducing the attack surface of a system by removing what is not needed and locking down what remains.
- Security follows **Defense in Depth** – multiple layers (network, user, file, service, logs).
- **Least privilege** – give users and services only the access they need.

## 🔥 Firewalls
| Distro | Tool | Example |
|--------|------|---------|
| RHEL / Rocky / Amazon Linux | `firewalld` | `sudo firewall-cmd --add-service=http --permanent && sudo firewall-cmd --reload` |
| Ubuntu | `ufw` | `sudo ufw allow 22/tcp && sudo ufw enable` |
| Low-level | `iptables` / `nftables` | `sudo nft list ruleset` |

> On cloud servers, also control access with **Security Groups / NSGs**.

## 🛡️ Mandatory Access Control
| Tool | Distro | Commands |
|------|--------|----------|
| **SELinux** | RHEL family | `getenforce`, `setenforce 0/1`, `sestatus`, `ls -Z`, `restorecon -Rv /path` |
| **AppArmor** | Ubuntu | `sudo aa-status` |

SELinux modes: **Enforcing** (blocks), **Permissive** (logs only), **Disabled**.
- Prefer fixing SELinux contexts over disabling SELinux.

## 🔐 Hardening Checklist
| Area | Action |
|------|--------|
| Updates | Patch regularly: `sudo dnf update -y` / `sudo apt upgrade -y` |
| SSH | Disable root login & password auth; use keys |
| Users | Remove unused accounts; lock idle users; strong password policy |
| Sudo | Limit sudo access; use groups (`wheel` / `sudo`) |
| Services | Disable unused services: `systemctl disable --now <svc>` |
| Ports | Check open ports: `ss -tulnp`; close what's not needed |
| Files | Check world-writable files & SUID binaries |
| Logs | Monitor `/var/log/secure` or `/var/log/auth.log` |
| Brute force | Use **fail2ban** to block repeated failed logins |
| Integrity | Use tools like AIDE to detect file changes |

## 💻 Useful Security Commands
```bash
last ; lastb                         # successful & failed logins
sudo grep "Failed password" /var/log/secure     # RHEL
sudo grep "Failed password" /var/log/auth.log   # Ubuntu
find / -perm -4000 -type f 2>/dev/null           # SUID files
find / -perm -0002 -type f 2>/dev/null           # world-writable files
sudo chage -l username                           # password ageing
sudo systemctl list-unit-files --state=enabled   # enabled services
```

## ❓ Interview Questions
1. What is server hardening? Name 5 steps.
2. What is SELinux? Explain its modes.
3. firewalld vs ufw vs iptables?
4. How do you find failed login attempts?
5. What is fail2ban?
6. Why are SUID files a security risk?

## 📝 Practice
- Harden an EC2 instance: update packages, disable root SSH login, enable firewall allowing only SSH & HTTP, install fail2ban, and list all SUID files.
