Find all files in a directory by file type:
> find /usr/share/doc -name "*.pdf"

Find all files edited/modified in a directory in the last # of days:
> find /home -type f -mtime -1
-type:
• f: Regular file (-type f)
• d: Directory (-type d)
• l: Symbolic link (-type l)
• b: Block special file (-type b)
• c: Character special file (-type c)
• p: Named pipe (FIFO) (-type p)
• s: Socket (-type s)

Find all files with a keyword:
keyword = hosts
> find / -type f -name "hosts"
When a lot of results are found, redirect the errors:
> find / -type f -name "hosts" 2> /dev/null
All errout results are redirected to the /dev/null file and the results that we have permissions for are displayed.

Find files by size:
> find /etc -type f -size +50k 2> /dev/null
(+50k = greater than 50k, -50k = less than)

By default, find prints the output. You can have it execute a command instead with -exec
> find /etc -type f -size +50k 2> /dev/null -exec ls -lh {} \;
The brace brackets is a place holder for the filename and each command must end in a semi-colon (;), which you protect from the shell using the backslash escape (\).

Find all files with a particular permission:
> find /usr/bin -perm /u+s
This will print all files with the SUID bit, but only file names.
-exec can be used here to use ls -l and view the full permission details:
> find /usr/bin -perm /u+s -exec ls -l {} \;
<img width="1424" height="212" alt="image" src="https://github.com/user-attachments/assets/b6b74c58-cc4e-4b6b-b729-b99b086a7cd6" />

