# Create a 1GB disk image
## dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024

This creates a 1 GB empty disk image file.

dd → Low-level copying tool.

if=/dev/zero → Input file is /dev/zero (a special device that outputs endless zeros).

of=/tmp/disk1.img → Output file is /tmp/disk1.img.

bs=1M → Block size = 1 megabyte.

count=1024 → Write 1024 blocks.

# Attach disk image to loop device
losetup -fP /tmp/disk1.img
losetup -a

# Create Physical Volume
pvcreate /dev/loop0

# Create Volume Group
vgcreate devops-vg /dev/loop0

# Verify Volume Group
vgs

# Create Logical Volume
lvcreate -L 500M -n app-data devops-vg

# Verify Logical Volume
lvs

# Create filesystem
mkfs.ext4 /dev/devops-vg/app-data

# Create mount point
mkdir /mnt/app-data

# Mount Logical Volume
mount /dev/devops-vg/app-data /mnt/app-data

# Check disk usage
df -h

# Extend Logical Volume
lvextend -L +200M /dev/devops-vg/app-data

# Resize filesystem
resize2fs /dev/devops-vg/app-data

# Verify new size
df -h /mnt/app-data


# What I Learned

LVM Architecture Structure
LVM works in layers: Physical Volume (PV) → Volume Group (VG) → Logical Volume (LV) → Filesystem → Mount point.

Difference Between LV and Filesystem Resize
Extending a Logical Volume does NOT automatically extend the filesystem. After lvextend, the filesystem must be resized using resize2fs.

Flexibility of LVM
LVM allows dynamic resizing of storage without recreating partitions, making it very powerful for production environments.
