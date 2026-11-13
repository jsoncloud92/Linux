A symbolic link (commonly known as a symlink or soft link) is a special type of file in Linux that serves as a shortcut to another file or directory. It works almost exactly like a shortcut icon on a Windows desktop.
Instead of containing actual data (like text or a program), a symlink contains a text string that tells the Linux system the file path to the original target. When you open, modify, or execute a symlink, the Linux kernel transparently redirects your action to the target file.

On most distros, the /bin directory is a symbolic link to /usr/bin and it contains binary files and executables.
> ls -ld /bin
<img width="1038" height="98" alt="image" src="https://github.com/user-attachments/assets/16e737fe-3b2f-460d-a351-62e89d08ea52" />
The file permissions start with an l to show the file type is a link.

If changing directory to a symbolic link like /bin, pwd will display only /bin
Use pwd -P to display the physical location.
<img width="786" height="156" alt="image" src="https://github.com/user-attachments/assets/524b7ffe-8484-47f9-905c-e0a1cc9e7193" />

When changing system settings such as the timezone, the symbolic link (if there is one) will update to the new settings file.

Create symbolic links:
> ln -s
> ln -s /usr/share/doc ~/doc
> ls-ld ~/doc
<img width="1362" height="128" alt="image" src="https://github.com/user-attachments/assets/b311c0b2-6fbf-4db6-9f7f-92091d251cdb" />

