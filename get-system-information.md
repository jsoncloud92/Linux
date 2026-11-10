Getting to know the Linux environment

Print the Kernel name:
> uname

Print the Linux Kernel version:
> uname -a

Use the ls GNU utility to list files that end with the name release in this directory.
> ls /etc/*release

Find information on the OS:
> cat /etc/*release

<img width="1454" height="658" alt="image" src="https://github.com/user-attachments/assets/d6f1d67a-69ce-4650-a7f4-6e9dcfab6676" />

View available Kernel versions in the /boot partition:
> ls -lah /boot

-l = View one file at a time
-a = View all files including hidden files
-h = View human readable file sizes

The initrd.img and vmlinuz boot files are symbolically linked (pointed) to boot files with this kernel version specified.

