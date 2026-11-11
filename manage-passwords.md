Change a user's password:
First specify user
> sudo passwd <username>
You are then prompted to enter a password

Change the password for the current shell user:
> passwd
Enter current password
Enter new password

Force a complex password:
1. Open the file - /etc/pam.d/common-password in nano
> sudo nano /etc/pam.d/common-password

Look for the line that starts with 'password'
<img width="926" height="81" alt="image" src="https://github.com/user-attachments/assets/7e938d74-c92b-4ce7-8efd-e802d596041b" />

You can add requirements to the end of the line such as minlen=10 to set the minimum password length to 10 characters.




