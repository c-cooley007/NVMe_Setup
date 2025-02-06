<h1>Kali Linux NVMe Drive Partitioning and Mounting </h1>

<!-- ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)
!-->
<h2>Description</h2>
This project involved partitioning and mounting a new NVMe drive on a Kali Linux system.  The lsblk command was used to initially view the block devices.  parted was then used to partition the NVMe drive (/dev/nvme0n1) with a GPT partition table and two primary ext4 partitions, each occupying 50% of the drive. The partitions were then mounted at mountnvme1 and mountnvme2 respectively.  lsblk, df -h, and fdisk -l were used to verify the partitioning and mounting process, displaying block device information, disk usage, and partition details.
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
<img src="https://i.imgur.com/LHoqk1d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We're using the 'parted' utility to interavtively manage the disk /dev/nvme0n1:  <br/>
<img src="https://i.imgur.com/ewR8v8p.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The first partition starts at the 1MiB offset, and both are formatted with the ext4 filesystem.  The drive's partition table is set to GPT.
Be sure to 'print' to display the current partition table of the drive, a good way to verify: <br/>
<img src="https://i.imgur.com/Mo6MOW1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
We're going to make the first partition of your NVMe drive accessible within the file system. Remember trust but verify:  <br/>
<img src="https://i.imgur.com/DUsvoeK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now we do the second partition:  <br/>
<img src="https://i.imgur.com/Mwt2p0F.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Finally we can verify the partitioning and mounting process you've performed:  <br/>
<img src="https://i.imgur.com/Flf42RN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
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
