# 04 – File & Directory Management, Links, Inodes

## 🎯 Objectives
- Create, copy, move, delete files/dirs
- Understand inodes, hard links and soft links

## 💻 Commands
```bash
touch file1.txt                 # empty file / update timestamp
mkdir dir1 ; mkdir -p a/b/c     # -p creates parents
cp file1 file2 ; cp -r dir1 dir2
mv old new                      # move or rename
rm file ; rm -r dir ; rm -rf dir   # ⚠️ -rf is dangerous
rmdir emptydir
file app.log                    # find file type
stat file1.txt                  # inode, size, timestamps
find / -name "*.log" -size +10M
find /var -type f -mtime -1
locate nginx.conf
```

## 📘 Theory: Inode
- An **inode** stores file metadata: size, owner, permissions, timestamps, data block pointers.
- Inode does **NOT** store the filename – the directory maps name → inode number.
- `ls -i` shows inode number; `df -i` shows inode usage.

## 🔗 Hard Link vs Soft Link
| Feature | Hard Link | Soft (Symbolic) Link |
|---------|-----------|----------------------|
| Command | `ln file hlink` | `ln -s file slink` |
| Inode | Same as original | Different inode |
| Original deleted | Still works | Breaks (dangling) |
| Directories | ❌ Not allowed | ✅ Allowed |
| Across filesystems | ❌ No | ✅ Yes |

## 🔑 Key Points
- Three timestamps: **atime** (access), **mtime** (content modified), **ctime** (metadata changed).
- `rm -rf /` destroys the system – always double-check paths.

## ❓ Interview Questions
1. What is an inode? What happens when inodes are full?
2. Hard link vs soft link?
3. How to find files larger than 100MB?

## 📝 Practice
- Create hard & soft links, delete the original, observe results.
