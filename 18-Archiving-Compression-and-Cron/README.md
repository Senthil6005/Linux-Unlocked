# 18 – Archiving, Compression & Job Scheduling (cron)

## 🎯 Objectives
- Take backups with tar and automate tasks with cron

## 📘 Theory Notes
- **Archive** = combine many files into one (tar).
- **Compress** = reduce size (gzip, bzip2, xz, zip).

## 💻 tar & Compression
```bash
tar -cvf backup.tar /etc            # create
tar -czvf backup.tar.gz /etc        # create + gzip
tar -cjvf backup.tar.bz2 /etc       # bzip2
tar -tvf backup.tar                 # list
tar -xvf backup.tar.gz -C /restore  # extract to dir
gzip file ; gunzip file.gz
zip -r app.zip app/ ; unzip app.zip
```
| Option | Meaning |
|--------|---------|
| c | create |
| x | extract |
| t | list |
| v | verbose |
| f | file name |
| z / j / J | gzip / bzip2 / xz |

## ⏰ cron – Scheduling
```
* * * * *  command
│ │ │ │ └── Day of week (0-7, Sun=0/7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```
| Expression | Meaning |
|-----------|---------|
| `0 2 * * *` | Every day 2 AM |
| `*/5 * * * *` | Every 5 minutes |
| `0 9 * * 1-5` | Weekdays 9 AM |
| `@reboot` | At every boot |

```bash
crontab -e ; crontab -l ; crontab -r
sudo crontab -u devuser -l
# Example: daily backup
0 1 * * * tar -czf /backup/etc-$(date +\%F).tar.gz /etc >> /var/log/backup.log 2>&1
```
- System cron: `/etc/crontab`, `/etc/cron.d/`, `/etc/cron.daily/`
- One-time job: `at` command
- Access control: `/etc/cron.allow`, `/etc/cron.deny`

## ❓ Interview Questions
1. Write a cron to run a script every Sunday at 3 AM.
2. Difference between tar and gzip?
3. How to extract a tar.gz to a specific folder?
4. Why escape `%` in crontab?

## 📝 Practice
- Schedule a cron that backs up `/etc` daily and deletes backups older than 7 days.
