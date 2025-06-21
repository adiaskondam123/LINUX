# Linux & VM Administration Guide

---

## 1. What is an Operating System (OS)?
- **OS**: Software that acts as an intermediary between computer hardware and users, managing hardware resources and providing services for application software.

## 2. What is Linux?
- **Linux**: An open-source, Unix-like OS based on the Linux kernel, widely used for servers, desktops, and embedded systems.

## 3. Difference Between OS and Kernel
- **OS**: Complete system software (kernel + user utilities + interfaces).
- **Kernel**: Core part of OS; handles hardware interaction, memory, process, and device management.

## 4. What is Hardware?
- Physical components of a computer (CPU, RAM, disk, motherboard, etc.)

## 5. Difference Between Windows and Linux
- **Windows**: Proprietary, GUI-focused, less customizable.
- **Linux**: Open-source, CLI-focused, highly customizable, better for servers.

---

## 6. Kernel & Types of Kernel
- **Kernel**: Manages hardware, processes, memory, and system calls.
- **Types**:
  - Monolithic (Linux)
  - Microkernel (Minix)
  - Hybrid (Windows NT)
  - Exokernel

## 7. Shell & Types of Shell
- **Shell**: Interface to interact with OS via commands.
- **Types**:
  - Bourne Shell (`sh`)
  - Bourne Again Shell (`bash`) - most common
  - C Shell (`csh`)
  - Korn Shell (`ksh`)
  - Z Shell (`zsh`)

---

## 8. Root File System Architecture
- **/bin, /sbin, /etc, /usr, /var, /home, /root, /tmp**
  - `/bin`: Essential user binaries
  - `/sbin`: System binaries
  - `/etc`: Config files
  - `/usr`: User programs
  - `/var`: Variable data
  - `/home`: User home dirs
  - `/root`: Root user home
  - `/tmp`: Temporary files

---

## 9. Linux Booting Process
1. BIOS/UEFI
2. Bootloader (GRUB/LILO)
3. Kernel loads
4. `init` or `systemd` starts
5. Services/daemons start
6. Login prompt

---

## 10. Root Password Recovery
1. Reboot and edit boot parameters (add `single` or `init=/bin/bash` to kernel line)
2. Mount root fs as read-write: `mount -o remount,rw /`
3. Reset: `passwd root`
4. Reboot

---

## 11. File & Directory Functionalities

### Basic Commands
```bash
mkdir test         # Create directory
pwd                # Print working directory
cd /path           # Change directory
rmdir test         # Remove empty directory
rm file            # Remove file
touch file         # Create empty file
cat file           # Display file contents
vi file            # Edit file using vi
hostname           # Show/set system hostname
ls                 # List files
date               # Show date/time
history            # Show command history
cp src dest        # Copy files/directories
mv src dest        # Move/rename
uname -a           # System info
arch               # Hardware name
```

---

## 12. /etc/passwd File, User & Group Management

- **/etc/passwd**: Stores user account info.
- **User Creation**: `useradd username`
- **Group Creation**: `groupadd groupname`
- **User Functions**: `usermod`, `passwd`, `id`
- **Group Functions**: `gpasswd`, `groups`
- **Sticky Bit**: `chmod +t dir` (prevents file deletion by others in a shared dir)

---

## 13. Sudoers File
- File: `/etc/sudoers`, use `visudo` to edit.
- Grants users/admins root privileges.

---

## 14. User Deletion & Text Utilities
- **Delete User**: `userdel username`
- **grep**: Search text
- **sort**: Sort lines
- **more, less**: Paginate output
- **head, tail**: Start/end of file

---

## 15. VM Snapshots & System Monitoring
- **Snapshots**: Save VM state (via hypervisor UI/CLI)
- **uptime**: Show system up-time
- **top**: Dynamic process list
- **ps**: Process status
- **who, whoami, who am i**: User info

---

## 16. File Permissions & Ownership
- **ls -l**: View permissions
- **chmod**: Change permissions
- **chown**: Change ownership
- **su – username / su username**: Switch user

---

## 17. File Systems
- **Types**: ext4, xfs, ntfs, etc.
- **Attaching Disk**: Attach via hypervisor, detected as `/dev/sdX`
- **Partitions**: `fdisk`, `parted`
- **Create FS**: `mkfs.ext4 /dev/sdX1`
- **Mount**: `mount /dev/sdX1 /mnt`
- **df**: Disk usage
- **partprobe**: Update kernel partition table
- **free**: Show RAM/swap

---

## 18. Connecting VMs & File Transfer
- **SSH**: `ssh user@ip`
- **Copy**: `scp file user@ip:/path`
- **rsync**: `rsync -avz file user@ip:/path`

---

## 19. Mounting & Unmounting
- **Mount**: `mount device mountpoint`
- **Unmount**: `umount mountpoint`

---

## 20. Manipulating Files with mount/umount
- After mounting, all regular file operations are possible (cp, mv, rm, etc.)

---

## 21. /etc/shadow File & Links
- **/etc/shadow**: Stores encrypted passwords.
- **Hard Link**: `ln file linkname`
- **Soft Link**: `ln -s target linkname`

---

## 22. SSH Key Generation & Passwordless Authentication
```bash
ssh-keygen            # Generate key
ssh-copy-id user@host # Copy pub key to server
```
- Now, SSH won’t prompt for a password.

---

## 23. Hidden Files & Directories
- Start with a dot (`.`). List with `ls -a`.

---

## 24. `tty`, `crontab`, `rsync`
- **tty**: Terminal info
- **crontab**: Schedule tasks (`crontab -e`)
- **rsync**: Efficient file transfer

---

## 25. YUM & RPM
- **YUM**: Package manager for RPM-based distros.
- **RPM**: Tool for installing RPM packages.

---

## 26. fallocate & nohup
- **fallocate**: Allocate disk space (`fallocate -l 1G file`)
- **nohup**: Run process immune to hangups (`nohup command &`)

---

## 27. Thin/Thick Provisioning, Swap File
- **Thin**: Allocates storage on demand.
- **Thick**: Allocates all storage up front.
- **Swap File**: `dd if=/dev/zero of=/swapfile bs=1M count=1024; mkswap /swapfile; swapon /swapfile`

---

## 28. chage & Password Policies
- **chage**: Manage password expiry (`chage -l user`)

---

## 29. tar Command
- **Create**: `tar -cvf archive.tar dir`
- **Extract**: `tar -xvf archive.tar`

---

## 30. inode, sed, awk
- **inode**: Data structure storing file metadata.
- **sed**: Stream editor for text (`sed 's/old/new/g' file`)
- **awk**: Pattern scanning/processing (`awk '{print $1}' file`)

---

## 31. Bash Scripting
```bash
#!/bin/bash
echo "Hello, World!"
```
- Save as `script.sh`, run with `bash script.sh` or `./script.sh` (after `chmod +x script.sh`).

---

**Tip:** Practice commands on a test VM/environment to reinforce learning!
