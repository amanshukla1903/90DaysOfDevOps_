# Day 13 – Linux Volume Management (LVM)

## Objective

Learn Linux Volume Management (LVM) to manage storage flexibly by creating, extending, and mounting logical volumes.  
---

# Environment Preparation

Switched to root user:  
sudo \-i  
OR  
sudo su  
Since no spare disk was available, a virtual disk was created:  
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024  
losetup \-fP /tmp/disk1.img  
losetup \-a

### Observation

A virtual disk image of 1 GB was created and attached as a loop device.  
---

# Task 1: Check Current Storage

Commands:  
lsblk  
pvs  
vgs  
lvs  
df \-h

### Observation

* lsblk displayed available block devices and partitions.  
* pvs, vgs, and lvs showed no existing LVM configuration.  
* df \-h displayed current filesystem usage.

### Why?

These commands help understand the current storage layout before making changes.  
---

# Task 2: Create Physical Volume

Command:  
pvcreate /dev/loop0  
Verify:  
pvs

### Observation

The loop device was successfully initialized as a Physical Volume (PV).

### Why?

A Physical Volume is the first building block of LVM.  
---

# Task 3: Create Volume Group

Command:  
vgcreate devops-vg /dev/loop0  
Verify:  
vgs

### Observation

Volume Group devops-vg was created successfully.

### Why?

A Volume Group combines one or more Physical Volumes into a storage pool.  
---

# Task 4: Create Logical Volume

Command:  
lvcreate \-L 500M \-n app-data devops-vg  
Verify:  
lvs

### Observation

A 500 MB Logical Volume named app-data was created.

### Why?

Logical Volumes act like virtual partitions and can be resized easily.  
---

# Task 5: Format and Mount

Format the Logical Volume:  
mkfs.ext4 /dev/devops-vg/app-data  
Create mount point:  
mkdir \-p /mnt/app-data  
Mount the volume:  
mount /dev/devops-vg/app-data /mnt/app-data  
Verify:  
df \-h /mnt/app-data

### Observation

The Logical Volume was successfully mounted and available for storage.

### Why?

Formatting creates a filesystem, and mounting makes it accessible to the operating system.  
---

# Task 6: Extend the Volume

Extend the Logical Volume:  
lvextend \-L \+200M /dev/devops-vg/app-data  
Resize the filesystem:  
resize2fs /dev/devops-vg/app-data  
Verify:  
df \-h /mnt/app-data

### Observation

The storage size increased successfully without recreating the volume.

### Why?

LVM allows storage expansion without repartitioning or downtime in many scenarios.  
---

# Key Learning

* Physical Volume (PV) is created from a disk or partition.  
* Volume Group (VG) combines storage from one or more PVs.  
* Logical Volume (LV) is created from a VG and behaves like a partition.  
* LVM makes storage management flexible and scalable.  
* Storage can be extended easily as application requirements grow.

---

# Commands Practiced

lsblk  
pvs  
vgs  
lvs  
df \-h  
pvcreate  
vgcreate  
lvcreate  
mkfs.ext4  
mount  
lvextend  
resize2fs  
---

# Conclusion

Today I learned the fundamentals of Linux Volume Management (LVM), including creating physical volumes, volume groups, and logical volumes. I also practiced formatting, mounting, and extending storage, which are important skills for managing production Linux servers and cloud environments.  
Keep Learning.  
Aman

