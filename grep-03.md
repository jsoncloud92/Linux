Using the command grep, list only the root user from the file /etc/passwd:
> grep 'root' /etc/passwd

List the currently logged in user from the /etc/passwd file, make use of the variable $USER:
> grep "$USER" /etc/passwd 

Count how many accounts are configured with the login shell /usr/sbin/nologin.
Note: Use grep -F to set text only (in other words, no regular expressions), protecting the / used in the file path, and use -c to count matching lines:
> grep -Fc '/usr/sbin/nologin' /etc/passwd

The command grep can be used to check configuration values from files. Often these files will have many lines, and being able to search for the correct setting is useful. You can count the total lines with grep using -c ''.

First, count the lines in the file /etc/ssh/ssh_config, and then search for the setting StrictHostKeyChecking:
> grep -c '' /etc/ssh/ssh_config
> grep 'StrictHostKeyChecking' /etc/ssh/ssh_config

As well as using text searches in grep, many other tools can make use of these searches. To show this, you will use the vim text editor to enter the file /etc/ssh/ssh_config directly at the line containing StrictHostKeyChecking. You will not edit the file, but the following will just show you the quick method of moving to the correct line:
> sudo vim +/StrictHostKeyChecking /etc/ssh/ssh_config
(You may need to press enter to continue to edit the file.) To exit the file, press :q!.

Returning to grep and using the file /etc/os-release, search for UBUNTU_CODENAME, and print only the code name value. You will use both grep and cut for this:

Notes:

By using grep -i, you can ignore case, which can be useful if you are not sure of the exact case.
Passing -d= to cut returns the second field delimited by the equality sign (=).
> grep -i ubuntu_codename /etc/os-release | cut -f2 -d=
This will output jammy.

Search the dictionary file /usr/share/dict/words for the word color. Searching for the text color, without regular expression metacharacters, shows the limitation of text-only searches:
> grep 'color' /usr/share/dict/words
You can enhance the search for the word color. Try looking first for lines starting with color (^color), before listing only the line containing the word color, so starting and ending with color (^color$):
> grep '^color' /usr/share/dict/words
> grep '^color$' /usr/share/dict/words
Using an enhanced regular expression (-E), you can search for an alternate spelling of color, namely colour. The ? metacharacter makes the previous character optional. The pattern '^colou?r$' makes the u optional, and matches on both color and colour. As the American English version of the dictionary is likely to have only the US spelling of color, you can add the alternate spelling to check that the regular expression works:
> echo 'colour' | sudo tee -a /usr/share/dict/words
> grep -E '^colou?r$' /usr/share/dict/words
