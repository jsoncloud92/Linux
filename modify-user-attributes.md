Change the home directory of a user:
> sudo usermod -d /home/directoryname <username>

Create the new home directory for the user:
> sudo mkdir /home/directoryname

Provide access to the directory for a group:
> sudo chown -R :groupname /home/directoryname

- The command above requires sudo privilege escalation.
- chown is used to change the ownership of files on Linux. chown means change ownership.
 -R is for recursive. With this option, the /home/dba directory and all items created inside it, will belong to members of the group.
- :grouname refers to the group we're giving control. The preceding : is important: - groupname means the groupname user! - :dba means the groupname group.

Prevent a user from logging in:
> sudo usermod -s /sbin/nologin kari


