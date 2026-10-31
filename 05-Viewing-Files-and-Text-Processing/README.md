# 05 – Viewing Files & Text Processing

## 🎯 Objectives
- Read files and filter/process text – the most used skill for log analysis

## 💻 Viewing Files
| Command | Use |
|---------|-----|
| `cat` | Show whole file |
| `less` / `more` | Page through file (`q` to quit, `/` to search) |
| `head -n 10` | First lines |
| `tail -n 20` | Last lines |
| `tail -f app.log` | **Follow live log** |
| `wc -l` | Count lines/words/chars |

## 💻 Text Processing
```bash
grep "error" app.log            # search text
grep -i -r -n -v -c "error" .   # ignore case, recursive, line no, invert, count
cut -d: -f1 /etc/passwd         # extract column
sort file ; sort -n ; sort -r
uniq -c                         # count duplicates (use after sort)
tr 'a-z' 'A-Z'                  # translate chars
awk -F: '{print $1,$3}' /etc/passwd
sed 's/old/new/g' file          # replace text
sed -i 's/8080/9090/' app.conf  # edit in place
diff file1 file2
```

## 📘 Theory: Redirection & Pipes
| Symbol | Meaning |
|--------|---------|
| `>` | Redirect output (overwrite) |
| `>>` | Append output |
| `<` | Input from file |
| `2>` | Redirect errors |
| `&>` / `2>&1` | Output + errors |
| `\|` | Pipe – output of one command → input of next |
| `tee` | Write to file AND screen |

- Streams: **0 = stdin, 1 = stdout, 2 = stderr**
- `/dev/null` = black hole (discard output)

## 🔑 Real-world Example
```bash
# Top 5 IPs hitting nginx
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head -5
```

## ❓ Interview Questions
1. How to watch a log file in real time?
2. Difference between `>` and `>>`?
3. What is `2>&1`?
4. Use of grep / awk / sed?

## 📝 Practice
- Count number of users in `/etc/passwd`, list only usernames sorted.
