List all configuration files:
> ls /etc/*.conf

Store the output in a file:
> ls /etc/*.conf > ~/conf.list

Listing the whole contents of /etc would give errors for files that a standard user does not have access to.
Redirect the errors to a file:
>ls -R /etc/ 2> ~/error
<img width="1438" height="280" alt="image" src="https://github.com/user-attachments/assets/b9cfebf8-d9a0-41ab-ab76-46c3b9b54952" />
-R = Recursively (Recursive means a process, rule, or function that repeats by applying itself to a smaller version of its own output or problem) This means subdirectories are also displayed.
- 2> = 2 specifies it is error output.
- 1> = This would have been used for standard output.
- Change 2> for 2>> to append an existing file.

View the contents of the file:
> cat ~/error
Tip:
The last argument was ~/error. Esc then . repeats the last argument.
> cat esc .
~/error will appear after cat, press enter to display the contents.

Redirection will not work for files that you do not have permissions for when opening the shell.
For example:
> sudo echo "8.8.8.8 google" >> /etc/hosts
<img width="1356" height="96" alt="image" src="https://github.com/user-attachments/assets/7a013701-93ad-4435-a372-36dcc2c45be3" />
To get around this, the tee command is used instead of > or >>
> echo "8.8.8.8 google" | sudo tee -a /etc/hosts
-a = append
View the last entry of the hosts file with:
> tail -n1 /etc/hosts

Redirect both standard output and error output to the same file:
> ls -l /etc/hosts /etc/hosts-2 &> output.txt
The file will contain a listing of the /etc/hosts file and an error saying that hosts2 does not exist.

