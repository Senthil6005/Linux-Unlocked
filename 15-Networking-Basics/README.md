# 15 – Linux Networking Basics

## 🎯 Objectives
- Check IPs, ports, connectivity and DNS – essential for troubleshooting

## 📘 Theory Notes
- **IP address:** identity of a machine (IPv4 `10.0.1.25`, IPv6).
- **Private ranges:** `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`
- **CIDR:** `/24` = 256 IPs; `/16` = 65,536 IPs
- **Port:** identifies a service on a machine (0–65535).
- **DNS:** converts names → IPs.

### Common Ports
| Port | Service |
|------|---------|
| 22 | SSH |
| 80 / 443 | HTTP / HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 8080 | Tomcat / Jenkins |
| 53 | DNS |
| 25 | SMTP |

### TCP vs UDP
| TCP | UDP |
|-----|-----|
| Connection-oriented, reliable | Connectionless, fast |
| HTTP, SSH, DB | DNS, streaming |

## 💻 Commands
```bash
ip a ; ip r                # IP addresses, routes (old: ifconfig, route)
hostname -I
ping -c 4 google.com
curl -I https://example.com ; wget url
ss -tulnp                  # listening ports (old: netstat -tulnp)
telnet host 3306 ; nc -zv host 3306   # port reachable?
traceroute google.com ; tracepath
nslookup google.com ; dig google.com
```

## 📄 Important Files
| File | Purpose |
|------|---------|
| `/etc/hosts` | Local name → IP mapping |
| `/etc/resolv.conf` | DNS servers |
| `/etc/hostname` | Machine name |

## 🔥 Firewall
```bash
sudo firewall-cmd --add-port=8080/tcp --permanent ; sudo firewall-cmd --reload   # RHEL
sudo ufw allow 8080/tcp ; sudo ufw status                                        # Ubuntu
```
> On AWS, also check **Security Groups** and NACLs.

## ❓ Interview Questions
1. How to check which ports are listening?
2. App not reachable – how will you troubleshoot?
3. What is /etc/hosts vs DNS?
4. TCP vs UDP?

## 📝 Practice
- Install nginx, verify port 80 with `ss`, curl it locally and from your browser.
