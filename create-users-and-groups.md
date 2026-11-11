Create a group:
> sudo addgroup <groupname>

Verify current user account:
> whoami

Add a user to a group:
> sudo usermod -aG <groupname> <username>
> sudo usermod -aG Finance jdoe

- sudo escalates your privilege, as you've seen before
- usermod allows you to modify the attributes of a user
- On Linux, a user may belong to one primary group, and many supplementary groups. The -a option instructs Linux to add supplementary group-membership for the user, without resetting the user's current group memberships. - For example, if the user was previously a member of the accounting group, using -a will add the user to the sre group, while preserving their membership in accounting as well. Without -a, the user will be removed from accounting, and added to only sre.
- The -G option accepts a comma-separated list of supplementary groups to which the user will be added. In our example, we've supplied only one supplementary group.
To add the current user in the shell to a group, you can use:
> sudo usermod -aG <groupname> $(whoami)

Create a user:
> sudo adduser --disabled-password --gecos "New SRE" jamie

adduser is an interactive command to create user accounts. - By default, it will prompt for quite a bit of information when creating a user account. Interactive commands are user-friendly, but interactivity often gets in the way of automation, which is why we've passed-in the additional options --disabled-password and --gecos for scriptability.
--disabled-password tells adduser to not ask for password during account creation. We can always set the password later.
--gecos allows us to supply extra information to describe the user account, in this case, New SRE.
Finally, we have the name of the user account - jamie.

View group information at /etc/group

When creating a user, they must be a member of one primary group. Therefore the /etc/group file will a group that has been created to be the primary group of the new user.

The information in /etc/group show the group name, unique ID, and users.

<img width="382" height="92" alt="image" src="https://github.com/user-attachments/assets/e05a7b08-97d3-436b-baed-a48b404d066a" />

Find information on a user account:
> grep jamie /etc/passwd

- In this example, we've asked grep to search /etc/passwd for any occurrence of the word jamie - The word jamie occurs only once in /etc/passwd
- jamie is the user
- x is deprecated. It's really a reminder that the user's password is stored elsewhere on the system
- 1002 is the unique user ID. Every user must have one. The root superuser has the UID of 0.
- 1003 is ID of the user's primary group
- The next field is essentially for commenting. It lets you to add extra information about the user such as their full name, phone number etc. In our case, the only comment is New SRE.
- /home/jamie is the home directory of the user. For comparison, on a Windows computer, the home directory would look something like C:\Users\pagaba where pagaba is my own username
- The final field holds whatever program we wish to automatically run anytime the user logs in. Most of the time, this program will be the user's default shell, for example /bin/bash, or /bin/zsh which is getting more and more popular these days. Truthfully though, it can be just about any program that's executable by the system. - In fact, we can prevent users from being able to login by pointing them to /sbin/nologin.

