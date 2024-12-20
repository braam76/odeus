
# ODEUS OS

This is a project I created while following [Linux From Scratch](https://www.linuxfromscratch.org/).

> **Disclaimer:**  
> If you want to follow my steps and create your own distribution as I did, ensure everything is compatible with your system.  
> (Especially if you're not using Alpine Linux, as package names and dependencies might differ.)

---

## Why?

There are three reasons why I started this project:

1. **Learning the Basics:**  
   I wanted to understand how distributions like Debian, Arch, Fedora, and openSUSE are built under the hood.

2. **Exploring Package Managers:**  
   I wanted to learn how package managers are created and how they download, compile, and manage packages.  
   *(I might even try to create my own package manager someday.)*

3. **Challenging Myself:**  
   I decided to challenge myself by creating an OS that could compete with giants like Debian, Arch, Fedora, and openSUSE.

---

## How I Started

I began by setting up a virtual machine where I installed Alpine Linux and configured two disks:

- **Disk 1:** Used to store the Alpine system.
- **Disk 2:** Dedicated to building ODEUS OS.

Below are the steps I followed. *(The numbers in parentheses indicate the corresponding steps from the Linux From Scratch guide.)*

---

## ODEUS Build Process

### Step 1: Host System Requirements (2.2)

I copied the `version_check.sh` script provided by Linux From Scratch.  
*(If needed, you can find it at `odeus/version_check.sh` in my repository.)*

---

### Step 1.1: Adjustments for Alpine Linux

Since I used Alpine as the host system, I needed to make some adjustments:

1. Install `bash` and relink `/bin/sh` from `busybox` to `/bin/bash`:
   ```bash
   doas ln -sf /bin/bash /bin/sh
   ```

2. Install the required packages for building LFS:
   ```bash
   doas apk add bash grep coreutils binutils bison findutils gawk gcc g++ gzip \
   m4 make patch perl python3 sed tar texinfo xz
   ```

---

### Step 2: Setting the `$ODEUS` Variable (2.6)

Define the location where the build system will be stored:
```bash
echo 'export ODEUS=/mnt/odeus' >> ~/.bashrc
source ~/.bashrc
```

**Note:**  
Always ensure the `$ODEUS` variable is set correctly, as an incorrect value can disrupt the entire build process.

---

### Step 3: Mounting the New Partition (2.7)

Prepare the second disk for the ODEUS build:

1. Format the disk as `ext4`:
   ```bash
   mkfs.ext4 /dev/sdb1
   ```

2. Create and mount the partition:
   ```bash
   mkdir -vp /mnt/odeus
   mount /dev/sdb1 /mnt/odeus
   ```

3. Verify the mount:
   ```bash
   df -h | grep /mnt/odeus
   ```

---

This is the beginning of the journey in building ODEUS OS!
