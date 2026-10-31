# 16 – SSH, Key-based Auth & File Transfer

## 🎯 Objectives
- Securely connect to servers and transfer files

## 📘 Theory Notes
- **SSH (Secure Shell)** – encrypted remote login on **port 22**.
- Server daemon: `sshd`; config: `/etc/ssh/sshd_config`; client config: `~/.ssh/config`.
- **Key-based auth** uses a key pair:
  - **Private key** – stays with you (never share)
  - **Public key** – placed on server in `~/.ssh/authorized_keys`

## 💻 Commands
```bash
ssh-keygen -t ed25519          # or -t rsa -b 4096
ssh-copy-id user@server
ssh user@server ; ssh -p 2222 user@server ; ssh -i key.pem user@ip

scp file.txt user@ip:/tmp/
scp -r dir user@ip:/opt/
scp user@ip:/var/log/app.log .
rsync -avz dir/ user@ip:/backup/   # sync only changes
sftp user@ip
```

## 🔐 Required Permissions
| Path | Permission |
|------|------------|
| `~/.ssh` | 700 |
| `~/.ssh/authorized_keys` | 600 |
| private key | 600 / 400 |

## 🛡️ SSH Hardening (`/etc/ssh/sshd_config`)
```
PermitRootLogin no
PasswordAuthentication no
Port 2222
AllowUsers senthil devuser
```
`sudo systemctl restart sshd` – keep the current session open while testing!

## ❓ Interview Questions
1. How does SSH key authentication work?
2. Difference between scp and rsync?
3. "Permission denied (publickey)" – how to fix?
4. How to disable root login?

## 📝 Practice
- Create 2 EC2s, set up passwordless SSH from one to other, copy files with scp & rsync.
