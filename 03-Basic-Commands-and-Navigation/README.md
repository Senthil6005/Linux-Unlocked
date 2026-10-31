# 03 – Basic Linux Commands & Navigation

## 🎯 Objectives
- Master everyday commands and command syntax

## 📘 Theory Notes
- **Command syntax:** `command [options] [arguments]` → `ls -l /etc`
- Options: short (`-l`) or long (`--all`); can combine `-la`.
- Help: `man <cmd>`, `<cmd> --help`, `whatis`, `apropos`.

## 💻 Important Commands
| Command | Use |
|---------|-----|
| `pwd` | Present working directory |
| `ls -l / -a / -h / -lt / -R` | List files (long, hidden, human size, by time, recursive) |
| `cd` | Change directory |
| `clear` / `Ctrl+L` | Clear screen |
| `history` | Previous commands (`!n`, `!!`) |
| `echo` | Print text / variable |
| `which`, `whereis`, `type` | Locate a command |
| `alias ll='ls -l'` | Create shortcut |
| `date`, `cal` | Date & calendar |
| `who`, `w`, `last` | Logged-in users / login history |

## ⌨️ Useful Shortcuts
| Key | Action |
|-----|--------|
| `Tab` | Auto-complete |
| `Ctrl+C` | Stop running command |
| `Ctrl+R` | Search history |
| `Ctrl+A / Ctrl+E` | Start / end of line |
| `Ctrl+D` | Logout / EOF |

## 🔑 Key Points
- `ls -l` output: `permissions links owner group size date name`
- File type first char: `-` file, `d` dir, `l` link, `c` char device, `b` block device

## ❓ Interview Questions
1. How to see hidden files?
2. How to find the full path of a command?
3. How to rerun the last command?

## 📝 Practice
- Create an alias, check `history`, use `man ls` to find 3 new options.
