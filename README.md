# Linux-Troubleshooting-Lab



## Local Setup Prerequisites (macOS)

Required software for running this lab on Apple Silicon Macs (M1/M2/M3):

1. **VMware Fusion Player** (Free for personal use)
2. **Ubuntu Desktop ARM64 ISO** (Required for MAC Apple Silicon compatibility)

---

## Step 1: Download Ubuntu ARM64 Version

* **For Apple Silicon Macs:** You MUST use ARM64 version
* **Download:** **Ubuntu 25.04 ARM64** from [ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)
* **Why ARM64?** Apple Silicon chips require ARM architecture - standard Intel/AMD versions will cause compatibility errors

---

## Step 2: Download VMware Fusion Player

* **Download:** https://www.vmware.com/products/fusion/fusion-evaluation.html
* **Select:** "Personal Use License" (Free)
* **Install:** Standard installation process

---

## Step 3: Create Virtual Machine

1. Open **VMware Fusion Player**
2. Drag and drop the **Ubuntu 25.04 ARM64 ISO file** into VMware window
3. Complete the on-screen installation steps to set the user account and finish the Ubuntu setup.

## Important Architecture Note

**Apple Silicon Requirement:** Standard x86_64 (Intel/AMD) Ubuntu versions are incompatible with Apple Silicon Macs and will throw architecture errors.

**If you see this error:** "The X86 machine architecture virtual machine is incompatible with the Arm machine architecture host"
- Solution: Use **Ubuntu ARM64 version only**

---

## Linux Skills to Practice

- Service management: `systemctl start/stop/restart apache2`
- File permissions: `chmod`, `chown`, `chgrp`
- Process monitoring: `ps`, `top`, `htop`, `kill`
- Network troubleshooting: `ping`, `curl`, `netstat`, `ss`
- Log analysis: `journalctl`, `tail -f`, `grep`
- User management: `adduser`, `passwd`, `usermod`
- Disk management: `df -h`, `du -sh`, `fdisk`

## Troubleshooting Common Issues

1. **Service won't start:** Check `systemctl status` and `journalctl`
2. **Permission denied:** Verify file permissions with `ls -la`
3. **Network issues:** Test connectivity with `ping` and `curl`
4. **Disk space:** Monitor with `df -h` and clean up with appropriate commands
