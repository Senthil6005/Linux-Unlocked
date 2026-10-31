# 19 – Shell Scripting Basics

## 🎯 Objectives
- Automate repetitive tasks with bash scripts

## 📘 Theory Notes
- **Shell script** = text file of commands executed in sequence.
- First line **shebang**: `#!/bin/bash` – tells which interpreter to use.
- Run: `chmod +x script.sh && ./script.sh` or `bash script.sh`

## 🧱 Building Blocks
```bash
#!/bin/bash
# Variables (no spaces around =)
NAME="Senthil"
echo "Hello $NAME"

# Command substitution
TODAY=$(date +%F)

# User input
read -p "Enter env: " ENV

# Arguments
echo "Script: $0, First arg: $1, All: $@, Count: $#"
echo "Exit status of last cmd: $?"
```
| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1..$9` | Arguments |
| `$#` | No. of args |
| `$@` / `$*` | All args |
| `$?` | Exit status (0 = success) |
| `$$` | PID of script |

## 🔀 Conditions
```bash
if [ -f /etc/passwd ]; then
  echo "File exists"
elif [ -d /tmp ]; then
  echo "Dir exists"
else
  echo "Not found"
fi
```
| Test | Meaning |
|------|---------|
| `-f` / `-d` / `-e` | file / dir / exists |
| `-z` / `-n` | string empty / not empty |
| `-eq -ne -gt -lt -ge -le` | numeric compare |
| `==` / `!=` | string compare |

## 🔁 Loops
```bash
for i in 1 2 3; do echo $i; done
for f in /var/log/*.log; do echo "$f"; done
COUNT=1
while [ $COUNT -le 5 ]; do echo $COUNT; ((COUNT++)); done
```

## ❓ Interview Questions
1. What is a shebang?
2. What does `$?` return?
3. Difference between `$@` and `$*`?
4. Write a script to check if a file exists.

## 📝 Practice
- Script that takes a username as argument and creates the user if not present.
