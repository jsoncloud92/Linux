It is recommended to use sudo rather than su to raise priviliges.
For security, password authentication for the root account can be locked.
Check the password status of root. An L indicates the password is locked:
> sudo passwd -S root

Admin rights and rights to specific commands can be delegated. Delegation is managed in the /etc/sudoers file or files in /etc/sudoers.d/

**Create a group and delegate rights**
Create the group:
> sudo groupadd helpdesk

Aim - allow helpdesk group to use sudo with the passwd command but not to change the password of root. Create a file to allow this:
Reference a group with %
> echo '%helpdesk ALL=(root) /usr/bin/passwd, !/usr/bin/passwrd root' > ~/helpdesk

Breakdown:
• %helpdesk: The % prefix tells sudo this rule applies to a user group named helpdesk rather than a single user.
• ALL=: Applies this rule to all hosts/machines using this configuration file.
• (root): Allows members of the group to run the specified commands as the root user.
• /usr/bin/passwd: Grants permission to execute the passwd utility (used to change passwords).
• , !/usr/bin/passwd root: The exclamation mark (!) acts as a negation, explicitly denying the ability to run passwd with root as the argument.

Check the file worked:
> visudo -cf ~/helpdesk

Once the file is created, set the ownership and permissions to root for user and group owner:
> sudo chown root.root ~/helpdesk
> sudo chmod u=rw,og=
With the correct permissions, copy the file to /etc/sudoers.d/
WARNING: If the file was not made correctly, this could break the sudo system on the machine.
> sudo cp -a ~/helpdesk /etc/sudoers.d/
-a = maintain permissions

Testing with a user:
You will now create a new user account named helpuser who is a member of the helpdesk group. Use the sudo useradd command for this. The option -m creates the user's home directory, -G helpdesk adds the user to the helpdesk group, -s /bin/bash sets the default shell to bash:

> sudo useradd -m -G helpdesk -s /bin/bash helpuser
Verify rights:
> sudo -lU helpuser
-l= list the allowed commands
-U = specify user

<img width="1462" height="364" alt="image" src="https://github.com/user-attachments/assets/2c9dc145-88e0-43bc-955e-ebbd03bcb1ab" />
