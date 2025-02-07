<h1>Kali Linux NVMe Drive Partitioning and Mounting </h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)
!-->
<h2>Description</h2>
This project involved partitioning and mounting a new NVMe drive on a Kali Linux system.  The lsblk command was used to initially view the block devices.  Parted was then used to partition the NVMe drive (/dev/nvme0n1) with a GPT partition table and two primary ext4 partitions, each occupying 50% of the drive. The partitions were then mounted at mountnvme1 and mountnvme2 respectively.  lsblk, df -h, and fdisk -l were used to verify the partitioning and mounting process, displaying block device information, disk usage, and partition details.
<br />


<h2>Languages and Utilities Used</h2>

- <b>COMMAND LINE INTERFACE, CLI</b> 
- <b>lsblk = list block devices</b>
- <b>parted = disk partitioning utility</b>
- <b>mklabel = part of the parted, used to set the disk label (GPT)</b>
- <b>mkpart = part of the parted, used to create partitions</b>
- <b>mkdir = make directory (for mount points)</b>
- <b>mount = mount a filesystem</b>
- <b>df = display disk space usage</b>
- <b>fdisk = disk partitioning utility (used for verification)</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Program walk-through:</h2>

<p align="center">
Launch the command line, 'sudo su' and 'lsblk' to display information about block devices: <br/>
<img src="https://i.imgur.com/LHoqk1d.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>

 <!-- Key Information:
NAME: The device name (e.g., /dev/sda, /dev/nvme0n1, /dev/sdb1). Devices without a number are usually the whole disk, while those with a number are partitions.
MAJ:MIN: The major and minor device numbers. These are used internally by the kernel. You usually won't need to worry about these.
RM: Whether the device is removable (1) or not (0).
SIZE: The total size of the device.
RO: Whether the device is read-only (1) or read-write (0).
TYPE: The type of block device (e.g., disk, part, rom, loop). disk is a whole disk, part is a partition.
MOUNTPOINT: The directory where the partition is mounted (if it's mounted). If it's not mounted, this will be blank.
!-->
<br />


<br />
We're using the 'parted' utility to interavtively manage the disk /dev/nvme0n1:  <br/>
<img src="https://i.imgur.com/ewR8v8p.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>

 <!--  Key Information
When you run parted /dev/nvme0n1, it starts parted in interactive mode.  You'll see a prompt where you can enter commands.  Here are some common parted commands:
print: Displays the current partition table.
mklabel <type>: Sets the partition table type (e.g., mklabel gpt, mklabel msdos). Warning: This will erase all existing partitions on the disk.
mkpart <type> <filesystem type> <start> <end>: Creates a new partition.
<type>: For GPT, this is a label (e.g., primary, data). For MBR, it's primary or extended.
<filesystem type>: The type of filesystem you intend to put on the partition (e.g., ext4, xfs, btrfs). This is just a hint; you still have to create the filesystem later with mkfs.
<start>: The starting point of the partition (e.g., 1MiB, 100GB).
<end>: The ending point of the partition (e.g., 50%, 200GB).
rm <number>: Deletes a partition (replace <number> with the partition number).
resizepart <number> <end>: Resizes a partition.
move <number> <start>: Moves a partition.
set <number> <flag> <state>: Sets or unsets a partition flag (e.g., set 1 boot on).
quit: Exits parted.
 --!>
<br />


<br />
The first partition starts at the 1MiB offset, and both are formatted with the ext4 filesystem.  The drive's partition table is set to GPT.
Be sure to 'print' to display the current partition table of the drive, a good way to verify: <br/>
<img src="https://i.imgur.com/Mo6MOW1.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>
<br />


<br />
We're going to make the first partition of your NVMe drive accessible within the file system. Remember trust but verify:  <br/>
<img src="https://i.imgur.com/DUsvoeK.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>

 <!-- Key Information
mkfs: This is the general command for making a filesystem.  It's a front-end for various filesystem-specific tools (like mkfs.ext4, mkfs.xfs, etc.)

-t ext4: This option specifies the type of filesystem to create.  ext4 is a very common and robust journaling filesystem used extensively in Linux. It's a good general-purpose choice.

/dev/nvme0n1p1: This is the device and partition that you are formatting.

/dev/nvme0n1: This refers to an NVMe (Non-Volatile Memory Express) drive. NVMe drives are SSDs that use the NVMe protocol, offering much faster speeds than traditional SATA SSDs.
--!>
<br />

<br />
Now we do the second partition:  <br/>
<img src="https://i.imgur.com/Mwt2p0F.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>
<br />
<br />
Finally we can verify the partitioning and mounting process you've performed:  <br/>
<img src="https://i.imgur.com/lVZhqxF.png" height="80%" width="80%" alt="VNVMe Disk Partitioning and Mounting"/>
<br />

 <!-- Key Information
 df = diskfree
Filesystem: The name of the filesystem (usually a device name like /dev/sda1 or a logical volume).  It can also be a special filesystem like tmpfs (for temporary files) or a loop device.
Size: The total size of the filesystem.
Used: The amount of space currently used on the filesystem.
Avail: The amount of space available on the filesystem.
Use%: The percentage of space used on the filesystem. This is a quick way to see how full a disk is.
Mounted on: The directory where the filesystem is mounted (the mount point).
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
