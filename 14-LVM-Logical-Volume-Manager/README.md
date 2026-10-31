# 14 – LVM (Logical Volume Manager)

## 🎯 Objectives
- Create flexible storage that can be resized online

## 📘 Theory Notes
- Normal partitions are fixed size. **LVM** lets you combine disks and **extend volumes without downtime**.

### LVM Layers
```
Physical Disks  (/dev/xvdf, /dev/xvdg)
      ↓  pvcreate
Physical Volumes (PV)
      ↓  vgcreate
Volume Group (VG)  – pool of storage
      ↓  lvcreate
Logical Volumes (LV) → format → mount
```
| Term | Meaning |
|------|---------|
| PV | Disk/partition initialized for LVM |
| VG | Pool of one or more PVs |
| LV | "Virtual partition" carved from VG |
| PE | Physical Extent – smallest chunk (default 4 MB) |

## 💻 Commands
```bash
sudo pvcreate /dev/xvdf /dev/xvdg
sudo vgcreate datavg /dev/xvdf /dev/xvdg
sudo lvcreate -L 3G -n applv datavg
sudo mkfs.xfs /dev/datavg/applv
sudo mount /dev/datavg/applv /app

pvs ; vgs ; lvs          # summary
pvdisplay ; vgdisplay ; lvdisplay

# Extend
sudo vgextend datavg /dev/xvdh
sudo lvextend -L +2G /dev/datavg/applv
sudo xfs_growfs /app            # xfs
sudo resize2fs /dev/datavg/applv   # ext4
# or in one step: lvextend -r -L +2G ...
```

## 🔑 Key Points
- xfs can **grow but not shrink**; ext4 can shrink (offline).
- LVM snapshots are useful for backups.

## ❓ Interview Questions
1. What is LVM and why use it?
2. Explain PV, VG, LV.
3. How to extend a logical volume online?

## 📝 Practice
- Create VG from 2 disks, LV of 3G, mount it, then extend by 1G.
