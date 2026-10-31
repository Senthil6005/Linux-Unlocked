# 10 – Process Management

## 🎯 Objectives
- Monitor, control and prioritize running processes

## 📘 Theory Notes
- **Program** = file on disk; **Process** = running instance with a **PID**.
- **PPID** = parent PID. `systemd` is PID 1, parent of all.
- **Daemon** = background service process (sshd, nginx).

### Process States
| State | Meaning |
|-------|---------|
| R | Running |
| S | Sleeping (waiting) |
| D | Uninterruptible sleep (I/O) |
| T | Stopped |
| Z | **Zombie** – finished but parent didn't collect exit status |

### Signals
| Signal | No. | Meaning |
|--------|-----|---------|
| SIGHUP | 1 | Reload config |
| SIGINT | 2 | Interrupt (Ctrl+C) |
| SIGKILL | 9 | Force kill (can't be caught) |
| SIGTERM | 15 | Graceful stop (default) |
| SIGSTOP | 19 | Pause (Ctrl+Z = SIGTSTP) |

## 💻 Commands
```bash
ps -ef ; ps aux | grep nginx
top ; htop                    # live view (load avg, CPU, mem)
pidof nginx ; pgrep nginx
kill -15 <PID> ; kill -9 <PID>
pkill nginx ; killall nginx
nice -n 10 ./script.sh        # start with priority
renice -5 -p <PID>            # change priority (-20 high .. 19 low)
./long.sh &                   # run in background
jobs ; fg %1 ; bg %1
nohup ./app.sh &              # survive logout
```

## 📘 Load Average
- `uptime` shows 1, 5, 15 min load. Load > number of CPU cores = overloaded.

## ❓ Interview Questions
1. Difference between kill -9 and kill -15?
2. What is a zombie process? Orphan process?
3. How to find which process uses most CPU/memory?
4. What is load average?

## 📝 Practice
- Run `sleep 1000 &`, find its PID, change priority, kill it.
