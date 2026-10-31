# 07 – User & Group Management

## 🎯 Objectives
- Create and manage users/groups and understand the files behind them

## 📘 Theory Notes
- Linux is **multi-user**. Every user has a **UID**, every group a **GID**.
| User type | UID range |
|-----------|-----------|
| root | 0 |
| System users (services) | 1 – 999 |
| Normal users | 1000+ |

- **Primary group:** one per user (default: same name as user).
- **Secondary groups:** extra groups for access (e.g., `docker`, `wheel`).

## 📄 Important Files
| File | Content |
|------|---------|
| `/etc/passwd` | User account info |
| `/etc/shadow` | Encrypted passwords & password ageing |
| `/etc/group` | Group info |
| `/etc/gshadow` | Group passwords |
| `/etc/skel` | Template files copied to new home dirs |
| `/etc/login.defs` | Default UID range, password policy |

`/etc/passwd` format:
```
username:x:UID:GID:comment:home_dir:shell
senthil:x:1001:1001:Trainer:/home/senthil:/bin/bash
```

## 💻 Commands
```bash
sudo useradd -m -s /bin/bash devuser
sudo passwd devuser
sudo usermod -aG docker devuser      # add to secondary group (-a is important!)
sudo usermod -L devuser / -U         # lock / unlock
sudo userdel -r devuser              # delete with home
sudo groupadd devops ; sudo groupdel devops
id devuser ; groups devuser
sudo chage -l devuser                # password ageing
su - devuser                         # switch user
```

## ❓ Interview Questions
1. What is stored in `/etc/passwd` vs `/etc/shadow`?
2. What is the UID of root?
3. Why use `-a` with `usermod -G`?
4. How to lock a user account?

## 📝 Practice
- Create group `devops`, 3 users in it, set password expiry 30 days.
