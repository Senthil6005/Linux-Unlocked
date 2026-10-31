# 20 – Advanced Scripting, Monitoring & Troubleshooting

## 🎯 Objectives
- Write production-style scripts and troubleshoot real server issues

## 🧱 Advanced Scripting
```bash
#!/bin/bash
set -euo pipefail          # exit on error, undefined var, pipe failure

# Functions
check_service() {
  if systemctl is-active --quiet "$1"; then
    echo "$1 is running"
  else
    echo "$1 is down – restarting"; sudo systemctl restart "$1"
  fi
}
check_service nginx

# Case
case "$1" in
  start) echo "Starting" ;;
  stop)  echo "Stopping" ;;
  *)     echo "Usage: $0 {start|stop}"; exit 1 ;;
esac

# Arrays
SERVICES=(nginx sshd crond)
for s in "${SERVICES[@]}"; do check_service "$s"; done
```

## 📜 Real DevOps Script – Disk Alert
```bash
#!/bin/bash
THRESHOLD=80
USAGE=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
if [ "$USAGE" -gt "$THRESHOLD" ]; then
  echo "ALERT: Disk usage is ${USAGE}% on $(hostname)"
fi
```

## 🩺 Monitoring Commands
| Area | Commands |
|------|----------|
| CPU / Load | `top`, `htop`, `uptime`, `mpstat` |
| Memory | `free -h`, `vmstat` |
| Disk | `df -h`, `du -sh`, `iostat`, `df -i` |
| Network | `ss -tulnp`, `ping`, `curl`, `dig` |
| Logs | `journalctl`, `/var/log/*`, `tail -f` |

## 🛠️ Troubleshooting Scenarios
| Problem | Approach |
|---------|----------|
| Server slow | `top` → high CPU/mem process, check load avg, `free -h` |
| Disk full | `df -h` → `du -sh /* | sort -h` → clean logs / extend LVM |
| Can't create file but space free | Inodes full → `df -i` |
| Website down | `systemctl status`, `ss -tulnp`, logs, firewall, Security Group |
| SSH fails | Port 22, SG, key permissions, `sshd` status, `/var/log/secure` |
| Service not starting at boot | `systemctl is-enabled`, `journalctl -b -u svc` |

## 🎓 Course Wrap-up – Linux for DevOps
- Linux is the base for **Docker, Kubernetes, Jenkins, Ansible, Terraform & AWS**.
- Key skills: files & permissions, users, processes, services, storage, networking, scripting.

## ❓ Interview Questions
1. What does `set -e` do?
2. How do you troubleshoot a slow server?
3. Disk shows space but cannot write – why?
4. Write a script to monitor and restart a service.

## 📝 Final Assignment
- Write a script that checks CPU, memory, disk and a service status, logs the report to `/var/log/health.log`, and schedule it with cron every 10 minutes.
