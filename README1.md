# Linux & VM Administration – In-Depth Guide with Diagrams

---

## 1. What is an Operating System (OS)?

**Definition:**  
An OS is software that manages computer hardware, software resources, and provides services for computer programs.

**Main Functions:**
- Resource management (CPU, memory, storage, devices)
- Process management (scheduling, multitasking)
- File management (reading, writing, organizing files)
- Security and access control
- User interface (CLI/GUI)

**ASCII Diagram:**
```
+---------------------+
|   Applications      |
+---------------------+
|  User Interfaces    |
+---------------------+
|      Kernel         |
+---------------------+
|     Hardware        |
+---------------------+
```

**Graphical Diagram:**  
Create a layered diagram (stacked rectangles) in [draw.io](https://draw.io/) or [diagrams.net](https://diagrams.net) with each component labeled as above.

---

## 2. What is Linux?

**Linux:**  
A family of open-source Unix-like operating systems based on the Linux kernel.

**Key points:**
- Kernel + utilities = Linux OS (distro)
- Common distributions: Ubuntu, CentOS, Fedora, Debian, Arch

---

## 3. OS vs Kernel

| OS (Operating System)   | Kernel                          |
|-------------------------|---------------------------------|
| Complete system         | Core system component           |
| Includes kernel, shell, utilities | Manages hardware resources      |
| Provides UI/UX          | No direct user interaction      |

**ASCII:**
```
[ Apps ] - [ Shell ] - [ Kernel ] - [ Hardware ]
```

---

## 4. Hardware

**Definition:**  
Physical components of a computer system.

**Examples:**  
CPU, RAM, Hard Disk, NIC, GPU

**Diagram:**
```
+----------------------+
| Motherboard          |
| +----+ +----+ +----+ |
| |CPU | |RAM | |HDD|  |
| +----+ +----+ +----+ |
+----------------------+
```

---

## 5. Windows vs Linux

| Windows | Linux |
|---------|-------|
| Closed source, paid license | Open source, free |
| GUI-focused | CLI-focused (but has GUIs) |
| Less customizable | Highly customizable |
| Used in desktops/gaming | Used in servers, embedded, devops |

---

## 6. Kernel & Types

**Kernel:**  
The bridge between applications and hardware.

**Types:**
- **Monolithic:** All system services in one large kernel (Linux)
- **Microkernel:** Minimal kernel, services in user space (Minix, QNX)
- **Hybrid:** Mix of both (Windows NT, macOS)
- **Exokernel:** Minimal abstraction, apps manage resources directly

**ASCII:**
```
Monolithic: [Kernel (All services)]
Micro:      [Kernel] <-> [User services]
```

---

## 7. Shell & Types

**Shell:**  
A program that interprets commands from the user.

**Types:**
- Bourne (sh)
- Bash (default on most Linux)
- Korn (ksh)
- C Shell (csh)
- Z Shell (zsh)

**Diagram:**  
```
[User] <-> [Shell] <-> [Kernel]
```

---

## 8. Root File System Architecture

**Key Directories:**
- /bin – essential binaries
- /sbin – system binaries
- /etc – configs
- /usr – user programs
- /var – variable data
- /home – user home dirs
- /root – root user home
- /tmp – temporary files

**ASCII:**
```
/
|-- bin/
|-- sbin/
|-- etc/
|-- usr/
|-- var/
|-- home/
|-- root/
|-- tmp/
```

**Graphical:**  
A tree diagram with root `/` branching to each directory.

---

## 9. Linux Boot Process

1. **BIOS/UEFI** – Hardware checks, finds bootloader  
2. **Bootloader (GRUB/LILO)** – Loads kernel  
3. **Kernel** – Hardware initialization  
4. **init/systemd** – Starts services  
5. **Login** – User access

**ASCII:**
```
[Power ON]
   |
[BIOS/UEFI]
   |
[Bootloader]
   |
[Kernel]
   |
[Init/Systemd]
   |
[Login]
```

---

## 10. Root Password Recovery

**Steps:**
1. Reboot, edit GRUB, append `single` or `init=/bin/bash`
2. Boot to shell, remount root: `mount -o remount,rw /`
3. `passwd root`
4. Reboot

---

## 11. File & Directory Operations

- **Create dir:** `mkdir dir1`
- **Create file:** `touch file1`
- **List:** `ls -l`
- **Change dir:** `cd dir1`
- **Remove file:** `rm file1`
- **Remove dir:** `rmdir dir1` or `rm -r dir1`
- **Copy:** `cp src dest`
- **Move/rename:** `mv src dest`
- **View:** `cat file1`, `less file1`
- **Edit:** `vi file1`

---

## 12. Basic Commands

See above, plus:
- `pwd`, `hostname`, `date`, `history`, `uname -a`, `arch`

---

## 13. /etc/passwd, Users & Groups

- **/etc/passwd:** User info
- **/etc/group:** Group info
- **User management:** `useradd`, `userdel`, `usermod`
- **Group management:** `groupadd`, `groupdel`
- **Sticky bit:** `chmod +t /shared`

---

## 14. Sudoers File

- **/etc/sudoers**, edit with `visudo`
- Grants root privileges to users/groups

**Example:**
```
rahul  ALL=(ALL)  ALL
```

---

## 15. User Deletion & Text Utilities

- `userdel username`
- `grep`, `sort`, `more`, `less`, `head`, `tail`

---

## 16. VM Snapshots & Monitoring

- **Snapshots:** Save/revert VM state (via VM software)
- **uptime, top, ps, who, whoami, who am i**

---

## 17. File Permissions & Ownership

- `ls -l` → `-rwxr-xr-x 1 root root file`
- `chmod 755 file`
- `chown user:group file`
- `su username` or `su - username`

**ASCII:**
```
Permissions: rwxr-xr-x
Owner:      root
Group:      root
```

---

## 18. File Systems

- **Types:** ext4, xfs, ntfs, vfat, etc.
- **Add disk in VM (shows as /dev/sdX)**
- **fdisk/parted:** Partition disk
- **mkfs.ext4 /dev/sdX1:** Format
- **mount /dev/sdX1 /mnt**

---

## 19. Connect VMs & Copy Data

- **SSH:** `ssh user@host`
- **SCP:** `scp file user@host:/path/`
- **rsync:** `rsync -avz dir/ user@host:/remote/`

---

## 20. Mounting & Unmounting

- `mount device mountpoint`
- `umount mountpoint`

---

## 21. Manipulate Files on Mounted FS

After mounting, use normal file operations on that mountpoint.

---

## 22. /etc/shadow & Links

- **/etc/shadow:** Encrypted passwords
- **Hard link:** `ln file newfile`
- **Soft link:** `ln -s file link`

---

## 23. SSH Keygen & Passwordless Auth

- Generate: `ssh-keygen`
- Copy: `ssh-copy-id user@host`
- SSH now won’t prompt for a password

---

## 24. Hidden Files

- Start with `.` (dot)
- List: `ls -a`

---

## 25. tty, crontab, rsync

- **tty:** Which terminal?
- **crontab:** Schedule jobs (`crontab -e`)
- **rsync:** Efficient file sync/transfer

---

## 26. YUM & RPM

- **YUM:** High-level package manager (`yum install nginx`)
- **RPM:** Low-level (`rpm -ivh pkg.rpm`)

---

## 27. fallocate & nohup

- **fallocate:** Preallocate disk space (`fallocate -l 1G file`)
- **nohup:** Run command immune to hangups (`nohup longjob &`)

---

## 28. Thin/Thick Provisioning & Swap

- **Thin:** Allocates space as used
- **Thick:** Allocates all space upfront
- **Swap:**  
  ```
  dd if=/dev/zero of=/swapfile bs=1M count=1024
  mkswap /swapfile
  swapon /swapfile
  ```

---

## 29. chage & Password Policies

- `chage -l user` (see policy)
- Set max days: `chage -M 30 user`

---

## 30. tar

- Create: `tar -cvf files.tar dir/`
- Extract: `tar -xvf files.tar`

---

## 31. Inode, sed, awk

- **inode:** Stores file metadata (not name)
- **sed:** Stream edit text (`sed 's/old/new/g' file`)
- **awk:** Pattern scanning/processing (`awk '{print $1}' file`)

---

## 32. Bash Scripting

**Example:**
```bash
#!/bin/bash
for file in *.txt; do
  echo "File: $file"
done
```
- Save, `chmod +x script.sh`, run with `./script.sh`

---

# Graphical Diagram Resources

- [draw.io](https://draw.io/) or [diagrams.net](https://diagrams.net): Free, easy, and recommended for IT/network/system diagrams.
- For **filesystem trees**: Use the "tree" shape and label branches.
- For **boot sequence**: Use a vertical flowchart with labeled boxes for BIOS, Bootloader, Kernel, Init, Login.
- For **permissions**: Use a table or a visual block explaining `rwx` for user/group/other.

---

**TIP:**  
Practice each command in a test VM, and try drawing the diagrams yourself for revision!
