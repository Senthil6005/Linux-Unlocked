# 12 – Services, systemd & Logs

## 🎯 Objectives
- Manage services with systemctl and read logs with journalctl

## 📘 Theory Notes
- **systemd** is the init system & service manager (PID 1) in modern Linux.
- It manages **units**:
| Unit type | Example |
|-----------|---------|
| `.service` | nginx.service |
| `.socket` | docker.socket |
| `.timer` | logrotate.timer (cron alternative) |
| `.target` | multi-user.target |
| `.mount` | data.mount |

- Unit file locations: `/usr/lib/systemd/system/` (package), **`/etc/systemd/system/`** (custom – higher priority)

## 💻 systemctl Commands
```bash
sudo systemctl start|stop|restart|reload nginx
sudo systemctl enable nginx      # start at boot
sudo systemctl disable nginx
sudo systemctl enable --now nginx
systemctl status nginx
systemctl is-active nginx ; systemctl is-enabled nginx
systemctl list-units --type=service
sudo systemctl daemon-reload     # after editing unit files
```
> `restart` = stop + start; `reload` = re-read config without stopping.

## 📄 Custom Service Example
`/etc/systemd/system/myapp.service`
```ini
[Unit]
Description=My Spring Boot App
After=network.target

[Service]
User=ec2-user
ExecStart=/usr/bin/java -jar /opt/app/app.jar
Restart=always

[Install]
WantedBy=multi-user.target
```

## 📜 Logs
```bash
journalctl -u nginx              # service logs
journalctl -u nginx -f           # follow
journalctl -b ; journalctl --since "1 hour ago"
ls /var/log                      # messages, secure, syslog, auth.log
```

## ❓ Interview Questions
1. Difference between start and enable?
2. Difference between restart and reload?
3. How to create a custom systemd service?
4. When do you run `daemon-reload`?

## 📝 Practice
- Install nginx, enable it, check status & logs; create a custom service for a script.
