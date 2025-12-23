# Getting Started with Kali Linux  
Installation, File System, and Basic Commands

Kali Linux is a Debian-based Linux distribution focused on security, penetration testing, and digital forensics. For learning and CTFs, the safest and most flexible way to use Kali is inside a **virtual machine (VM)** rather than directly on hardware.

---

## 1. Prerequisites

- 64-bit CPU with virtualization enabled (Intel VT-x / AMD-V in BIOS/UEFI).  
- At least **8 GB RAM** and **40–60 GB** free disk recommended for smooth usage.  
- Stable internet connection to download images and tools.

---

## 2. Install Kali Linux in Virtual Machines (Recommended)

### 2.1 Choose Your Virtualization Platform

- **Windows / Linux / Intel‑Mac:** Oracle **VirtualBox**.  
- **Apple Silicon Mac (M1/M2/M3/M4):** **UTM**.

> For this guide, VirtualBox and UTM are the primary focus.

---

### 2.2 Kali Linux on VirtualBox (Win / Linux / Intel‑Mac)

#### Step 1 – Install VirtualBox

1. Go to VirtualBox downloads: https://www.virtualbox.org/wiki/Downloads.  
2. Download the installer for your host OS (Windows, macOS, or Linux).  
3. Run the installer and accept defaults unless you have specific needs.

#### Step 2 – Get Kali for VirtualBox

You have **two** convenient options:

- **Option A – Prebuilt Kali VM (fastest)**  
  1. Open: https://www.kali.org/get-kali/#kali-virtual-machines.  
  2. Download the **VirtualBox** image (`.7z`) for your architecture.  
  3. Extract the archive.  
  4. In VirtualBox, click **Add** → choose the extracted `.vbox` file to import the VM.

- **Option B – Install from ISO (more customizable)**  
  1. Download Kali ISO: https://www.kali.org/get-kali/ (Installer image).  
  2. In VirtualBox, click **New** and configure:
     - Name: `Kali-Linux`
     - Type: `Linux`, Version: `Debian (64-bit)`.  
     - RAM: at least **2–4 GB** for light work; **4–8 GB** recommended.  
     - CPUs: 2+ vCPUs if available.  
     - Disk: create a **VDI** with **40+ GB** dynamic size.  
  3. Start the VM and attach the Kali ISO when prompted.

#### Step 3 – Run the Graphical Installer (Option B)

Inside the VM boot menu:

1. Select **Graphical install**.  
2. Choose language, region, and keyboard layout.  
3. Set **hostname** and an optional **domain name**.  
4. Create a normal user and password (root is no longer default in latest releases).  
5. Partitioning:
   - Use **Guided – use entire disk** inside the VM (safe, does not touch host disk).  
   - Accept default partitioning scheme and write changes.  
6. Allow installation of the **GRUB bootloader** to the virtual disk so the VM boots Kali correctly.  
7. After installation completes, click **Continue** to reboot into Kali.

#### Step 4 – Post‑Installation Tweaks (VirtualBox)

- Log in with the user created during installation.  
- Open a terminal and update the system:

  ```
  sudo apt update
  sudo apt full-upgrade -y
  ```

- (Optional) Install **VirtualBox Guest Additions** to improve display, clipboard, and file sharing: mount the Guest Additions ISO from **Devices → Insert Guest Additions CD image** and follow the standard Linux steps.

---

### 2.3 Kali Linux on UTM (Apple Silicon Macs)

For M1/M2/M3/M4 Macs, UTM is the easiest free option.

#### Step 1 – Install UTM

1. Download UTM for macOS: https://mac.getutm.app or direct `.dmg` from the UTM GitHub releases.
2. Open the `.dmg` and drag **UTM.app** into **Applications**.

#### Step 2 – Get Kali for Apple Silicon

You can:

- Download a **ready‑made Kali UTM image** from the UTM gallery: https://mac.getutm.app/gallery/kali-2023 or newer.
- Or download **Kali ARM64 installer ISO**: https://www.kali.org/get-kali/#kali-installer-images (select ARM64 / Apple Silicon).

#### Step 3 – Create and Configure the UTM VM

If using an ISO:

1. Open **UTM** → **Create New**.  
2. Select **Virtualize** (for ARM on Apple Silicon). 
3. Choose **Linux** as the OS, then:
   - Attach the Kali ARM64 ISO.  
   - Allocate **4+ GB RAM** and **2–4 CPUs** depending on your Mac.  
   - Create a disk of at least **40–60 GB**.  
4. Start the VM and run the **Graphical install** similar to the VirtualBox steps above.

If using a UTM gallery image:

1. Download the Kali UTM file from the gallery.
2. Double‑click it to import into UTM.  
3. Adjust RAM/CPU if needed, then start the VM.

#### Step 4 – First Boot and Updates

Inside Kali on UTM:

```
sudo apt update
sudo apt full-upgrade -y
```

Then configure networking, full-screen display, and shared folders according to the UTM documentation.

---

### 2.4 Optional: Kali with WSL (Windows 10/11)

If you want a terminal‑only Kali environment inside Windows:

1. Enable **WSL** and **Virtual Machine Platform** via `optionalfeatures.exe` or PowerShell.
2. Install WSL:

   ```
   wsl --install
   ```

3. From Microsoft Store, search for **Kali Linux** and install it.  
4. Launch Kali from Start menu, create a user, and then update:

   ```
   sudo apt update
   sudo apt full-upgrade -y
   ```

> WSL Kali is useful for CLI tools but does not give a full desktop experience without extra configuration.

---

## 3. Installing Kali as Dual‑Boot

> **Warning:** Dual‑boot modifies physical disks. Always backup important data first.

### 3.1 Dual‑Boot with Windows

High‑level flow (details vary by device):

1. **Backup** your Windows data to external storage. 
2. Download Kali installer ISO: https://www.kali.org/get-kali/.
3. Create a **bootable USB** using tools like Rufus / Win32 Disk Imager.
4. In Windows, shrink an existing partition to free at least **20–40 GB** for Kali using Disk Management.  
5. Boot from the Kali USB by changing boot order in BIOS/UEFI.  
6. Choose **Graphical install** and when partitioning:
   - Use **Guided – use the largest continuous free space** to avoid overwriting Windows.
7. Allow GRUB bootloader installation to the main disk so you can choose between Windows and Kali at boot.

Official docs: https://www.kali.org/docs/installation/dual-boot-kali-with-windows/.

### 3.2 Dual‑Boot with Other Linux Distros

Process is similar: resize the existing Linux partition with a tool like **GParted** from the Kali installation media, leaving free space for Kali.

Official docs: https://www.kali.org/docs/installation/dual-boot-kali-with-linux/.

---

## 4. Installing Kali as Primary OS (Bare Metal)

Using Kali as the only OS is **not** recommended for beginners or daily drivers, but it is possible.

### High‑Level Steps

1. Backup everything on the target disk.  
2. Create a bootable USB from the Kali installer ISO.  
3. Boot from the USB, choose **Graphical install**.  
4. When partitioning:
   - Use **Guided – use entire disk** (this erases the disk).
5. Install GRUB to the disk, complete installation, reboot into Kali.

Hard‑disk install docs: https://www.kali.org/docs/installation/hard-disk-install/ (and Mac‑specific variants).

---

## 5. Basic Kali Linux Filesystem Overview

Linux uses a hierarchical **single root** filesystem starting at `/` (root directory). A few important locations:

- `/` – Root of the filesystem, contains all directories.  
- `/home` – User home directories (`/home/student`, `/home/kali`, etc.).  
- `/root` – Home directory for the root user.  
- `/etc` – System‑wide configuration files.  
- `/bin`, `/usr/bin` – Essential user binaries and general applications.  
- `/sbin`, `/usr/sbin` – System administration binaries (often need sudo).  
- `/var` – Variable data like logs (`/var/log`), packages, caches.  
- `/tmp` – Temporary files, usually cleared on reboot.  

Kali inherits this structure from Debian, so most Debian/Ubuntu filesystem documentation applies.

---

## 6. Essential Terminal Commands for Kali Beginners

All commands below are run in a **terminal** inside Kali.

### 6.1 Navigation and Files

```
pwd          # Show current directory
ls           # List files
ls -la       # List with details including hidden files
cd /path     # Change directory
cd ~         # Go to your home directory
mkdir lab    # Create a directory
rmdir old    # Remove empty directory
rm file      # Remove file
rm -r dir    # Remove directory (recursive)
cp src dst   # Copy file
cp -r a b    # Copy directory
mv old new   # Move/rename
```

### 6.2 System Info and Management

```
whoami       # Show current user
id           # Show user and group IDs
uname -a     # Kernel and architecture info
hostname     # System hostname
uptime       # System uptime and load
df -h        # Disk usage
free -h      # RAM usage
top          # Live process view (press q to exit)
htop         # Better process viewer (install if missing)
```

### 6.3 Package Management (APT)

```
sudo apt update                   # Refresh package list
sudo apt full-upgrade -y          # Upgrade all packages
sudo apt install nmap -y          # Install a tool
sudo apt remove toolname -y       # Remove a tool
sudo apt search keyword           # Search packages
```

### 6.4 Permissions and Ownership

```
ls -l file                        # Show permissions
chmod 755 script.sh               # Change permissions (rwxr-xr-x)
chown user:group file             # Change owner and group (needs sudo)
sudo -i                           # Become root (interactive shell)
```

### 6.5 Networking Basics

```
ip a                               # Show IP addresses
ping 8.8.8.8                       # Check network connectivity
ip route                           # Show routing table
ss -tulpn                          # Show listening ports
```

---

## 7. Good Practices for Kali in Labs

- **Always update** before labs: `sudo apt update && sudo apt full-upgrade -y`.  
- Use **snapshots** in VirtualBox/UTM before major changes so you can roll back.  
- Avoid using Kali as your daily OS; treat it as a lab/attack box.  
- For assignments/CTFs, keep a separate **workspace directory** inside your home folder (`~/labs`, `~/ctf`, etc.).

---

## 8. Quick Decision Table

| Scenario                          | Recommended Method           | Notes |
|----------------------------------|------------------------------|-------|
| Beginner on Windows              | VirtualBox + Kali VM        | Safest, easy reset via snapshots. |
| Beginner on Apple Silicon Mac    | UTM + Kali ARM64/UTM image  | Optimized for M1/M2/M3/M4. |
| Need full desktop on Windows but no repartition | Kali VM (VirtualBox) | Better than WSL for GUI tools. |
| CLI‑only tools on Windows        | Kali on WSL                 | Lightweight but limited GUI. |
| Dedicated lab machine            | Dual‑boot or primary install| Only if comfortable with partitioning. |

---

> **Next step for sessions:** Ensure everyone comes with a working Kali VM (VirtualBox or UTM) plus basic familiarity with terminal navigation (`cd`, `ls`, `pwd`) and `apt` commands.