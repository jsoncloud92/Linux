OBJECTIVE 2
Interacting with text streams
Move to the /usr/share/doc directory and take a look at the current contents.

cd /usr/share/doc
ls
Use ls to list the contents of the git/ subdirectory.

ls git
Print the contents of the README.source file inside the git/ directory and use grep to filter for the string extracted. The single line containing the search string will be printed to the screen.

cat git/README.source | grep extracted
The problem is that just one line will often not give you enough information to understand the content in its proper context.

Add the -A flag to grep with the value of 2 to print the two lines that come after the matching line.

cat git/README.source | grep -A 2 extracted
If you need to see the lines that come before the matching line, use the -B flag along with some value instead of -A.

cat git/README.source | grep -B 5 extracted
If you want to see both lines before and after the matching line, use the -C (context) flag.

cat git/README.source | grep -C 4 extracted
Run ps along with the aux arguments to list all the processes currently active on your machine.

ps aux
This will show you each process along with information like the user who owns it, its process ID (PID), resource usage, and the original command that was used to execute the process.

Use grep to filter the output. This can be particularly useful when there are many hundreds of active processes in your system.

ps aux | grep root
You can specify where in the source text a search string should appear using special character arguments. The ^ character tells grep to return only lines that begin with (in this case) the word root.

ps aux | grep ^root
This allows us to narrow down the output to just the root user.

The $ character will work similarly by telling grep to return only lines that end with a specified character (or characters).

ps aux | grep d$
That example can be useful because it returns only processes that executed using a systemd service (whose names commonly end in the letter d).

You now have enough grep tools to do some serious administration work using both file system objects and text streams.
