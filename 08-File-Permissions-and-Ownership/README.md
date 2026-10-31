# 08 – File Permissions, Ownership & Special Permissions

## 🎯 Objectives
- Control who can read, write and execute files

## 📘 Theory Notes
`-rwxr-xr-- 1 senthil devops 120 Oct 31 app.sh`
| Part | Meaning |
|------|---------|
| `-` | File type |
| `rwx` | **User (owner)** |
| `r-x` | **Group** |
| `r--` | **Others** |

| Permission | File | Directory | Value |
|-----------|------|-----------|-------|
| r | Read content | List contents | 4 |
| w | Modify | Create/delete files | 2 |
| x | Execute | Enter (cd) | 1 |

Common values: `755` (rwxr-xr-x), `644` (rw-r--r--), `600` (rw-------), `400` (pem keys)

## 💻 Commands
```bash
chmod 755 app.sh ; chmod u+x,g-w,o-r file
chown senthil:devops file ; chown -R user:group dir
chgrp devops file
umask            # default 0022 → files 644, dirs 755
```

## 📘 umask
- Default max: files **666**, dirs **777**. Final = max − umask.

## ⭐ Special Permissions
| Permission | Value | Symbol | Effect |
|-----------|-------|--------|--------|
| SUID | 4 | `s` in user x | Runs as file owner (e.g., `/usr/bin/passwd`) |
| SGID | 2 | `s` in group x | Runs as group / new files inherit dir group |
| Sticky bit | 1 | `t` in others x | Only owner can delete files (e.g., `/tmp`) |
```bash
chmod 4755 file ; chmod 2775 dir ; chmod 1777 /shared
```

## 📘 ACL (Access Control Lists)
```bash
setfacl -m u:devuser:rw file
getfacl file
setfacl -x u:devuser file
```

## ❓ Interview Questions
1. What does 755 mean?
2. What is umask?
3. What are SUID, SGID and sticky bit? Give examples.
4. Why does SSH key need 400 permission?

## 📝 Practice
- Create a shared dir for group `devops` with SGID + sticky bit.
