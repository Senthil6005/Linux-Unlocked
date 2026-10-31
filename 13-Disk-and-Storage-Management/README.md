# 13 – Disk & Storage Management

## 🎯 Objectives
- Add a new disk, partition, format, mount and make it permanent

## 📘 Theory Notes
- Disks appear in `/dev`: `sda`, `xvda`, `nvme0n1` (AWS Nitro), partitions `sda1`, `nvme0n1p1`.
- Flow: **Disk → Partition → Filesystem (format) → Mount**

### Partition tables
| MBR | GPT |
|-----|-----|
| Max 2 TB | Up to 9.4 ZB |
| 4 primary partitions | 128 partitions |
| `fdisk` | `gdisk` / `parted` |

### Filesystems
| FS | Notes |
|----|-------|
| ext4 | Default in Ubuntu |
| xfs | Default in RHEL / Amazon Linux |
| swap | Virtual memory |
| vfat / ntfs | Windows compatible |

## 💻 Commands
```bash
lsblk ; blkid ; sudo fdisk -l
sudo fdisk /dev/xvdf          # n, p, w
sudo mkfs.ext4 /dev/xvdf1     # or mkfs.xfs
sudo mkdir /data
sudo mount /dev/xvdf1 /data
sudo umount /data
df -h                          # disk usage per filesystem
du -sh /var/log/*              # folder sizes
```

## 📄 /etc/fstab (permanent mount)
```
UUID=xxxx-xxxx   /data   ext4   defaults,nofail   0 0
```
Fields: device, mount point, fs type, options, dump, fsck order
- Always test with `sudo mount -a` – wrong fstab can stop boot!

## 🔑 Swap
```bash
sudo fallocate -l 1G /swapfile ; sudo chmod 600 /swapfile
sudo mkswap /swapfile ; sudo swapon /swapfile ; free -h
```

## ❓ Interview Questions
1. Steps to add a new EBS volume to EC2?
2. Difference between df and du?
3. What is /etc/fstab? Why use UUID?
4. MBR vs GPT? ext4 vs xfs?

## 📝 Practice
- Attach 2 GB EBS volume, format, mount at `/data`, persist via fstab.
