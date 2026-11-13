Understanding default permissions on newly created files and directories:
umask = user file-creation mode mask
The umask controls the default permissions assigned to newly created files and directories.
The default depends on the distro. e.g. defaults will differ in RHEL to Ubuntu.
The purpose is to protect data from the moment it is created. Every file is applied the umask and it can be removed if the permissions should be changed.

Umask	New File Permissions	New Directory Permissions	Common Use Case
0022	0644 (rw-r--r--)	0755 (rwxr-xr-x)	Standard on RHEL/Fedora; group/others can read but not write.
0002	0664 (rw-rw-r--)	0775 (rwxrwxr-x)	Standard on Ubuntu/Debian; group has write access.
0027	0640 (rw-r-----)	0750 (rwxr-x---)	Group can read; others have no access.
0077	0600 (rw-------)	0700 (rwx------)	Private; only the file owner has read/write access.

After creating a new file, ls -l will show the permissions which are not the defaults.
To view the defaults:
> umask -S

<img width="1046" height="240" alt="image" src="https://github.com/user-attachments/assets/5da92a6b-4a89-4f17-9733-f2d867ea0da8" />

Stop blocking default permissions:
> umask -S ugo=rwx
ugo = users, groups, others
Each will be set to read, write, execute on the directory. The umask for this would be 0000

<img width="1130" height="434" alt="image" src="https://github.com/user-attachments/assets/15c6df83-51a5-44da-95b5-5c08c7a7d7f7" />

By default, files get -rw-rw-rw-

Make a file more private by blocking permissions to groups and others:
> umask -S u=rwx,go=
A new directory will get rwx------ and a new file will get rw-------

The umask applies to the current shell session only. You can make it permanent by adding umask #### to ~/.bashrc

Permissions in Linux are NOT cumulative, if the user owns the file they will collect permissions granted to the user, and will NOT collect permissions granted to the group or others, even if they are a member of the group.
This means that if I create a file and the permissions are r--rwxrwx I cannot write to the file or even if I am a member of the group that has rwx.

<img width="1448" height="280" alt="image" src="https://github.com/user-attachments/assets/195f7eb0-52ad-4a04-80f6-f0a94faf013b" />

Deleting the file is still allowed if the user has write permissions to the directory

To run a script (./myscript) you must have execute permission to the script file.
<img width="1450" height="170" alt="image" src="https://github.com/user-attachments/assets/64fa139c-247f-46ed-9921-d90d02ff43e7" />
a+x = add execute to all blocks (ugo)

The execute permission on a directory is required to enter the directory. The read permission is helpful, allowing you to list the directory contents, however, it is not required if the user knows the name of the file, and has read permission on the file. This is good security, allowing users access to filenames that have been shared with them, but preventing them from locating other files.


TASK:
1. Create a group called shared in the root directory

2. Using `` sudo `` and `` chgrp ``, change the group owner of the new directory to the group `` sudo ``\. Your user `` pslearner `` is a member of this group\. Setting the group owner allows permissions assigned to the group to be used by the `` sudo `` group\.

3. Using `` sudo `` and `` chmod ``, set the group permissions to execute\-only\. You need to elevate permissions to use `` chmod ``, as you are not the owner of the in this case\.

4. Using `` sudo `` and `` cp ``, add the `` /etc/hosts `` file to the `` /shared `` directory\.

5. Working as your own user account, try to list the contents of the `` /shared `` directory using `` ls ``\. This will fail, as you only have execute, and not read, which is required to read or list the directory content\.

6. Now try to list the contents of the `` /shared/hosts `` file using `` cat ``\. This will work as you have execute to the directory and read to the file

Commands:
sudo mkdir /shared
sudo chgrp sudo /shared
sudo chmod g=x /shared
sudo cp /etc/hosts /shared
ls /shared
cat /shared/hosts

