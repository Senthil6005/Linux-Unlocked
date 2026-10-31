# 11 – Package Management

## 🎯 Objectives
- Install, update and remove software on RHEL & Debian systems

## 📘 Theory Notes
- **Package** = compiled software + metadata (`.rpm` or `.deb`).
- **Repository** = online store of packages.
- **High-level tools** (yum/dnf/apt) resolve **dependencies** automatically; low-level tools (rpm/dpkg) don't.

| | RHEL / Amazon Linux | Ubuntu / Debian |
|-|---------------------|-----------------|
| Package format | .rpm | .deb |
| Low-level | `rpm` | `dpkg` |
| High-level | `yum` / `dnf` | `apt` |
| Repo config | `/etc/yum.repos.d/` | `/etc/apt/sources.list` |

## 💻 Commands
```bash
# RHEL / Amazon Linux
sudo yum install -y git ; sudo dnf install nginx
sudo yum remove httpd ; sudo yum update -y
yum list installed ; yum search java ; yum info nginx
rpm -qa | grep java ; rpm -ivh pkg.rpm ; rpm -ql nginx

# Ubuntu / Debian
sudo apt update             # refresh repo index
sudo apt upgrade -y
sudo apt install -y nginx ; sudo apt remove nginx ; sudo apt purge nginx
apt list --installed ; apt search docker
sudo dpkg -i pkg.deb ; dpkg -l
```

## 🔑 Key Points
- `apt update` = refresh list; `apt upgrade` = install newer versions.
- `purge` removes config files too.
- Other install methods: `snap`, source (`./configure && make && make install`), binaries in `/opt`.

## ❓ Interview Questions
1. Difference between rpm and yum?
2. Difference between apt update and apt upgrade?
3. How to check if a package is installed?
4. Where are yum repos configured?

## 📝 Practice
- Install git, nginx, tree, java on both Amazon Linux and Ubuntu.
