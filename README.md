# Linux Troubleshooting Lab: Setup Guide & Command Reference



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

![Drag and Drop VM Installation](Linux/vm%20installation%20drag%20drop2.png) 


## Note

**Apple Silicon Requirement:** Standard x86_64 (Intel/AMD) Ubuntu versions are incompatible with Apple Silicon Macs and will throw architecture errors.

**If you see this error:** "The X86 machine architecture virtual machine is incompatible with the Arm machine architecture host"
![Architecture Incompatibility Error](Linux/error.png)
- Solution: Use **Ubuntu ARM64 version only**

---

##  Linux Fundamentals - Deep Explanations

## 1. Command Line Basics

**What is the Command Line?**
- Think of it as "text messaging" your computer
- Instead of clicking icons, you type commands
- More powerful than GUI - you can do things faster

**Understanding the Prompt:**
```bash
[username@computer ~]$
```

- $ = regular user (you)
- # = root user (administrator - be careful!)

To exit: Type exit or close the window


### Basic Command Structure
```text
command [options] [arguments]
```

### Essential Shell Features
| Feature | Control | Description |
|---------|---------|-------------|
| TAB completion | Press Tab | Type part of command → Auto-complete |
| Command history | Up/down arrows, Ctrl+R | Navigate and search history |
| Background jobs | Add & | Run program in background (e.g., firefox &) |
| Pausing | Ctrl+Z to pause, fg to resume, bg for background | Manually manage running processes |


### Getting Help
**Manual Pages (Man Pages)**
```bash
man commandname
```
Navigation: Spacebar (next page), /searchterm (search), q (quit)


### Other Help Commands
```bash
whatis command      # Brief description
apropos keyword     # Find commands about a topic
```

## 2. Hardware Management
**CPU Information**
```bash
lscpu               # Detailed CPU info (architecture, core count)
uname -a            # System info including architecture and kernel version
```

**Hardware Detection**
```bash
lspci               # List all PCI devices (graphics, network, etc.)
lsblk               # Show disks and partitions
```

**Disk Types & Filesystems**
- Disk Types: SATA/USB: /dev/sda; NVMe: /dev/nvme0.

- Partitioning: MBR (Max 2TB) vs. GPT (Modern, large disks).

- Filesystems: ext4 (Default Linux), XFS (For large files), Btrfs (Advanced features).

**Mounting Drives**
CRITICAL: Always unmount before removing USB drives!
```bash
umount /mount/point
```

## 3. File Management
### Essential Navigation
```bash
pwd                 # Show current directory ("Print Working Directory")
ls                  # List files
cd directory        # Change directory
```

### File Operations
```bash
touch filename      # Create empty file
cp file1 file2      # Copy file
mv old new          # Move/rename file
rm filename         # Delete file (PERMANENT - no trash!)
```

### Directory Management
```bash
mkdir folder        # Create directory
mkdir -p a/b/c      # Create nested directories
rmdir folder        # Remove EMPTY directory only
rm -r folder        # Remove directory and contents (Recursive)
```

### Important Directories (File System Hierarchy)
| Directory | Purpose |
| :--- | :--- |
| / | Root directory |
| /home | User files |
| /etc | Configuration files (**CRITICAL**) |
| /tmp | Temporary files |
| /var | Variable data (logs, etc.) (**CRITICAL**) |


File Paths
Absolute Path: /home/user/file.txt (Starts from root)

Relative Path: Documents/file.txt (From current location)

Home shortcut: ~/Documents

Wildcards

Wildcard,Description
*,Match any characters
?,Match single character
[],Match specific characters

4. Searching and Processing Data
Regular Expressions (RegEx)
^ - Start of line

$ - End of line

. - Any single character

* - Zero or more repetitions

+ - One or more repetitions

? - Zero or one occurrence

Search Commands
grep pattern file    # Search inside files
grep -r pattern dir  # Recursive search
find dir -name "*.txt"  # Find files by name


Data Processing Utilities
wc file              # Word count
cut -d: -f1 file     # Extract fields
sort file            # Sort lines
cat file1 file2      # Concatenate files


Redirection and Pipes
command > file       # Overwrite output to file
command >> file      # Append output to file
command 2> error.log # Redirect errors only
command < input.txt  # Redirect input

command1 | command2  # Pipe output to another command
ls -l | grep txt | wc -l  # Chain multiple commands

5. Process and Package Management
Viewing Processes

ps aux               # Show all processes
top                  # Live process monitor
free -h              # Memory usage

Service Management (Systemd)
systemctl status apache2   # Check service status (CRITICAL for troubleshooting)
systemctl start apache2    # Start a service
systemctl stop apache2     # Stop a service

Package Management (Debian/Ubuntu)
sudo apt update      # Update package lists
sudo apt install pkg # Install package
sudo apt remove pkg  # Remove package

6. User and Security
Account Types
Root: UID 0, full system access

System: UID 1-999, service accounts

User: UID 1000+, regular users

Account Files
/etc/passwd - User account details

/etc/shadow - Encrypted passwords

/etc/group - Groups

Security Commands
whoami               # Current user
id                   # User identity
sudo command         # Run single command as root (SAFE)
sudo -i              # Interactive root session
su -                 # Switch to root (Less safe)

File Permissions
Permission,Symbol,Octal Value
Read,r,4
Write,w,2
Execute,x,1

Changing Permissions and Ownership
chmod 755 file       # Octal method (rwxr-xr-x)
chmod u+x file       # Symbolic method (add execute to owner)
chown user:group file# Change owner and group

7. Scripting Basics (Automation Foundation)
Script Structure
#!/bin/bash
# Your commands here
echo "Hello World"

Execution
chmod +x script.sh   # Make script executable
./script.sh          # Run script

Variables and Arguments
name="John"
echo "Hello $name"
echo "First argument: $1"
echo "All arguments: $@"

Conditionals
if [ -f "$file" ]; then
    echo "File exists"
else
    echo "File not found"
fi

Loops
for file in *.txt; do
    echo "Processing $file"
done

count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done




pwd = "Print Working Directory" - shows where you are now

ls = "List" - shows what's in the current folder

cd = "Change Directory" - moves you to another folder

 Examples:

```bash
$ pwd
/home/john
$ ls
Documents Downloads Music
$ cd Documents
$ pwd
/home/john/Documents
```


#shortcuts
Symbolic Links (Shortcuts)
symbolic links (or symlinks) as the final file type (l).

The Goal: Create a simple name in your home folder that points to a distant folder, /usr/share/doc.

The Command: ln -s /usr/share/doc Doc

ln -s: Link, symbolic (this is the command to create the shortcut).

/usr/share/doc: The target (the real directory).

Doc: The name of the shortcut in your current folder.

The Benefit: You can then type cd Doc and instantly jump to that complicated path without taking up extra disk space.

---

## Troubleshooting Common Issues

1. **Service won't start:** Check `systemctl status` and `journalctl`
2. **Permission denied:** Verify file permissions with `ls -la`
3. **Network issues:** Test connectivity with `ping` and `curl`
4. **Disk space:** Monitor with `df -h` and clean up with appropriate commands
