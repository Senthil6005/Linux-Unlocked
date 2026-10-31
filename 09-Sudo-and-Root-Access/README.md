# 09 – Root, sudo & Privilege Management

## 🎯 Objectives
- Give admin rights safely using sudo

## 📘 Theory Notes
- **root** = superuser with unlimited power. Logging in as root directly is a security risk.
- **sudo** = run a single command with root privileges; actions are logged.
- **su** = switch to another user (needs that user's password).
| | `su -` | `sudo` |
|-|--------|--------|
| Password needed | Target user's | Your own |
| Scope | Full shell | Single command |
| Logging | Minimal | Logged (`/var/log/secure` or `auth.log`) |

## 📄 /etc/sudoers
- Always edit with **`visudo`** (checks syntax – broken file = no sudo!).
```
senthil   ALL=(ALL)       ALL
devuser   ALL=(ALL)       NOPASSWD: ALL
%devops   ALL=(ALL)       /usr/bin/systemctl restart nginx
```
Format: `user  host=(run_as)  commands`
- Drop-in files: `/etc/sudoers.d/devuser`
- Admin groups: **wheel** (RHEL/Amazon Linux), **sudo** (Ubuntu)

## 💻 Commands
```bash
sudo -i            # root shell
sudo -l            # what can I run?
sudo usermod -aG wheel devuser
sudo visudo
```

## ❓ Interview Questions
1. Difference between `su` and `sudo`?
2. Why use `visudo` instead of vim?
3. How to give a user passwordless sudo?
4. How to allow only one command via sudo?

## 📝 Practice
- Allow group `devops` to restart only nginx without password.
