# 01 – Linux Installation, Access & Boot Process

## 🎯 Objectives
- Set up a Linux lab (VM / AWS EC2)
- Connect using SSH
- Understand the Linux boot process

## 📘 Theory Notes
### Ways to get a Linux lab
- **Virtual Machine:** VirtualBox / VMware with Ubuntu or Rocky ISO
- **Cloud:** AWS EC2 (Amazon Linux / Ubuntu) – recommended for DevOps training
- **WSL:** Windows Subsystem for Linux

### Connecting to a server
```bash
ssh -i mykey.pem ec2-user@<public-ip>   # Amazon Linux
ssh -i mykey.pem ubuntu@<public-ip>     # Ubuntu
chmod 400 mykey.pem                     # key must not be world-readable
```

### 🔄 Linux Boot Process (6 Stages)
| # | Stage | What happens |
|---|-------|--------------|
| 1 | **BIOS / UEFI** | Power-On Self Test (POST), finds boot device |
| 2 | **MBR / GPT** | Boot sector loads the bootloader |
| 3 | **GRUB2** | Bootloader – shows menu, loads kernel + initramfs |
| 4 | **Kernel** | Initializes hardware, mounts root filesystem |
| 5 | **systemd (PID 1)** | First process; starts all services |
| 6 | **Target (runlevel)** | multi-user.target (CLI) or graphical.target (GUI) |

### Runlevels vs systemd targets
| Runlevel | Target | Meaning |
|----------|--------|---------|
| 0 | poweroff.target | Shutdown |
| 1 | rescue.target | Single user |
| 3 | multi-user.target | CLI, multi-user |
| 5 | graphical.target | GUI |
| 6 | reboot.target | Reboot |

## 💻 Commands
```bash
systemctl get-default
sudo systemctl set-default multi-user.target
sudo reboot ; sudo shutdown -h now ; sudo poweroff
dmesg | less        # kernel boot messages
```

## ❓ Interview Questions
1. Explain the Linux boot process.
2. What is GRUB? What is initramfs?
3. What is PID 1 in modern Linux?
4. Difference between MBR and GPT?

## 📝 Practice
- Connect to EC2 with SSH, check default target, view `dmesg`.
