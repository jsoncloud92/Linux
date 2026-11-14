The purpose of special permissions is to avoid users deleting data that they are not the owner of.
This is achieved using the "sticky bit"

To control deletions on a shared directory you can make use of the special permission known as the sticky bit. Special permissions do not have their own block to display in, and make use of the **x** block of the user, group, or others. The sticky bit occupies the others execute permission using the letter t. A lowercase t shows that execute is set, and uppercase T indicates that the execute permission is NOT set for others. If the sticky bit is set on a directory, files may only be deleted by the owner of the file. By default these permissions are set on the /tmp directory.

Example setup - /shared directory in root:
<img width="1080" height="204" alt="image" src="https://github.com/user-attachments/assets/d63a9680-a77f-48de-b426-9453a9d3359d" />
With my user, I can delete files in the /shared directory.

Add the sticky bit:
> sudo chmod o+t /shared
Create files to test:
> sudo touch /shared/root
> touch /shared/ps

Remove the new files:
> rm /shared/*

<img width="1236" height="200" alt="image" src="https://github.com/user-attachments/assets/7edc3566-d66c-48d4-a76f-907b12c31fe1" />

root is the owner of /shared/root so my user cannot delete this without sudo.
/shared/ps has been deleted as my user was the creator/owner.

We also want the group owner of the directory to be the group owner of new files within it.
This is achieved with the GUID bit (SGID):
Use u(user), g(group), or o(others) +s with chmod.

> sudo chmod g+s /shared
Create one file with sudo and one without.
> ls -l /shared
As sudo is the group owner for /shared, both files now show sudo as the group owner.

The SUID bit can also be set on executable files, as can the SGID bit. These special permissions control the execution context for a binary file. This sets the user or group context to be that of the user or group owner, respectively. Users can change their own passwords, and those passwords are stored in the file /etc/shadow. Users do not have access to this file. Try listing the file ls -l /etc/shadow or cat /etc/shadow. However, look at the permissions of the binary /usr/bin/passwd. The user block includes the lowercase s, indicating that the SUID bit set.

<img width="1130" height="246" alt="image" src="https://github.com/user-attachments/assets/6efc1cf7-37e4-4052-9bf6-ccd7982c762a" />

With the SUID bit configured on the /usr/bin/passwd file, the program executes as the file's owner, root. The program itself manages security, and allows users to only change their own password.

Wrap-up:

<img width="1338" height="960" alt="image" src="https://github.com/user-attachments/assets/5c5cb2f2-f172-4fc8-b1b6-d751e6cc3df4" />

Sticky bit use case:
Public folders that require everyone to have write permission but restricts accidental deletion.

SUID bit use case:
Allow standard users to run commands as root temporarily (files only). Execute as a user owner (root)

SGID use case:
Shared directories, execute as group owner.
