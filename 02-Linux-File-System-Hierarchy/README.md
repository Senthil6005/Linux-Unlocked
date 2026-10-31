# 02 – Linux File System Hierarchy (FHS)

## 🎯 Objectives
- Understand the Linux directory structure and purpose of each directory

## 📘 Theory Notes
- Linux has a **single tree** starting at root `/`. No C:/ D:/ drives.
- Other disks are **mounted** into this tree (e.g., `/mnt`, `/data`).

## 📂 Important Directories
| Directory | Purpose |
|-----------|---------|
| `/` | Root of the entire filesystem |
| `/root` | Home directory of root user |
| `/home` | Home directories of normal users |
| `/bin`, `/usr/bin` | User commands (ls, cp, cat) |
| `/sbin`, `/usr/sbin` | System admin commands (fdisk, useradd) |
| `/etc` | **Configuration files** (passwd, hosts, ssh) |
| `/var` | Variable data – **logs (`/var/log`)**, mail, cache |
| `/tmp` | Temporary files (cleared on reboot) |
| `/boot` | Kernel & GRUB files |
| `/dev` | Device files (sda, null, tty) |
| `/proc` | Virtual FS – running process & kernel info |
| `/sys` | Virtual FS – hardware/device info |
| `/opt` | Optional / third-party software |
| `/mnt`, `/media` | Mount points |
| `/lib`, `/lib64` | Shared libraries |
| `/usr` | User programs & data (read-only) |

## 🔑 Key Points
- **Absolute path:** starts with `/` → `/etc/ssh/sshd_config`
- **Relative path:** from current dir → `../logs/app.log`
- `.` = current dir, `..` = parent dir, `~` = home dir
- Hidden files start with `.` (e.g., `.bashrc`)

## 💻 Commands
```bash
pwd ; cd / ; ls -l
cd ~ ; cd - ; cd ..
cat /proc/cpuinfo ; cat /proc/meminfo
tree /etc  (install tree)
```

## ❓ Interview Questions
1. Where are logs stored? Where are config files stored?
2. What is `/proc`? Is it on disk?
3. Absolute vs relative path?

## 📝 Practice
- Visit each directory in the table and list its contents.
