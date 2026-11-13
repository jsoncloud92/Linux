Identify the Linux distro being used:
> hostnamectl

Print your username, ID and group memberships :
> ID

Return just your username:
> whoami

View your connection in detail:
> who am i

User connection details with CPU usage:
> w

List the terminal you are connected to:
> tty
Output example: /dev/pts/1

To see extended metadata of the terminal:
> ls -l /dev/pts/1
Shortcut:
> ls -l $(tty)

Get the date:
> date
Short form:
> date +F%
More variations can be found with man date

Copying a file and adding the date to the name of the file:
> cp /etc/hosts ~/hosts.$(date +F%)
The file is copied to the home directory and called hosts.<date>

<img width="1278" height="154" alt="image" src="https://github.com/user-attachments/assets/8e80e983-dcd4-40db-ad37-30e8c971a290" />

View the date in calendar output:
Current month:
> cal
Previous, current and next month:
> cal -3
A particular month and year:
> cal 9 1992
This would show September 1992

SSH connection details:
> echo $SSH_CONNECTION

Using cut to display only the information needed:
> echo $SSH_CONNECTION | cut -f1 -d" "
Where field 1 was the client IP address, we used cut to only display field 1 and specified that the fields are separated with a space (delimiter)
-f = field
-d = delimiter e.g. comma, space, etc. in quotes ","


