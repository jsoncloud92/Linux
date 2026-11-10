Explore Linux File System Directories, Disks, and Partitions

The Linux file system starts with the "root" directory (not to be confused with the root user). The root directory is simply /

View the contents of the root directory:
> ls -lah /
>
> -l = One line at a time
> -a = All files including hidden files
> -h = Human readable format

You can see a few symbolic links defined here, which are similar to shortcuts or pointers. The /bin directory is linked ( indicated by -> ) to usr/bin, for example.

The /boot directory contains boot files and kernel files.

The /etc directory often contains configuration files for system packages and other software.

The /home directory is used to store the home directories for the various system users. User specific files are stored here. The /home directory is often split out to its own partition, as the data can be quite variable and grow to a large size.

The /opt directory contains "optional" software, and is the location that is often used for installing additional software on the system by System Administrators.

The /var directory contains "variable" files and is most often used to store logs. This is another directory that is often partitioned off on its own, due to the aggressive file size growth that commonly occurs here.

**Block Devices**
In Linux, block devices are storage devices that provide random access to fixed‑size blocks—such as HDDs, SSDs, NVMe drives, USB storage, and loop devices—typically exposed under /dev/ (e.g., /dev/sda, /dev/nvme0n1) and managed through the kernel’s block layer subsystem.

**Loop Devices**
In Linux, /dev/loop entries represent loop devices — virtual block devices that map a regular file to behave like a physical disk. This allows the system to mount and access the file as if it were a real storage device.

Check the partitions on a disk:
> sudo fdisk -l /dev/nvme0n1 (Block device name)

Check file system disk space used:
> df -h
-h = Human readable


