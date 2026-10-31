# 06 – Text Editors: Vim & Nano

## 🎯 Objectives
- Edit configuration files confidently on servers

## 📘 Theory Notes
- Servers have no GUI → editing is done with **vi/vim** or **nano**.
- `vi` is available on almost every Linux system.

## 🔄 Vim Modes
| Mode | How to enter | Purpose |
|------|--------------|---------|
| Normal / Command | `Esc` | Navigate, copy, delete |
| Insert | `i`, `a`, `o` | Type text |
| Visual | `v`, `V` | Select text |
| Ex / Last-line | `:` | Save, quit, search-replace |

## ⌨️ Important Vim Commands
| Command | Action |
|---------|--------|
| `:w` / `:q` / `:wq` / `:q!` | Save / quit / save+quit / quit without save |
| `:x` or `ZZ` | Save & exit |
| `dd` / `5dd` | Delete line(s) |
| `yy` / `p` | Copy line / paste |
| `u` / `Ctrl+r` | Undo / redo |
| `gg` / `G` | Top / bottom of file |
| `:20` | Go to line 20 |
| `/word`, `n` | Search, next match |
| `:%s/old/new/g` | Replace all |
| `:set nu` | Show line numbers |

## 💻 Nano
```bash
nano file.txt   # Ctrl+O save, Ctrl+X exit, Ctrl+W search
```

## ❓ Interview Questions
1. How to exit vim without saving?
2. How to replace a word in the whole file in vim?
3. How to go to a specific line?

## 📝 Practice
- Create `/tmp/app.conf`, add 10 lines, replace a word, delete 3 lines, save.
