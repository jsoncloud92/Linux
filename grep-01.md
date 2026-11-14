OBJECTIVE 1
Finding objects anywhere within a Linux file system
Connect to the Ubuntu Desktop you'll be using and click on the Terminal icon at the bottom of the screen to open a terminal shell session.

Move to the /usr/share/doc directory which is where many software providers store configuration files. Then run ls to list the contents of the directory.

cd /usr/share/doc
ls
Running grep copyright to search for all files containing the word copyright will fail.

grep copyright
This happens because grep, when it's run like this, expects searchable text via standard input (stdin) - but this command doesn't provide any. You can escape the failed command by typing CTRL+c.

Add the -r flag to the grep command so it will search recursively for all the files in the current directory tree that contain the text copyright.

grep -r copyright
That command gave you many lines of output containing the subdirectory and filename where the text was found, along with all lines where the search string is found. Here's an example of output that you should see:

libblockdev-fs3/copyright:Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
libical3t64/copyright:Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
libical3t64/copyright: Redistributions of source code must retain the above copyright notice, this
libical3t64/copyright: Redistributions in binary form must reproduce the above copyright notice,
Add the l flag to that command if you want grep to print nothing more than the directory and file names.

grep -rl copyright
This is often all the information you need and it can be a lot easier for you to read.

Piping the output to the wc command will print just the number of lines, words, and characters in the output. This can be useful to get a sense of shape of your data in its current state.

grep -r copyright | wc
This information can help you decide whether you need to apply further filters.

Using the uppercase -R flag instead of the lowercase -r will recursively return even objects that are symbolic links.

grep -R copyright | wc
Note the difference between the number of lines here as opposed to the number of lines in the previous command. It can be important to distinguish between real objects and symbolic links to know how to maintain resources in your file system.

Run the two previous commands one more. But this time, instead of piping the output to wc, write them to two new files in your home directory (represented by the ~/ characters.

grep -r copyright > ~/lowercase.txt
grep -R copyright > ~/uppercase.txt
Run diff to print out all the lines that are in the uppercase.txt file but not in the lowercast.txt file.

diff ~/lowercase.txt ~/uppercase.txt
Those extra lines represent each of the instances where the search string (copyright) appear in directories that are just symbolic links. Here's an example of how the output (towards the bottom) might look:

> debconf-i18n/copyright:Format: https://www.debian.org/doc/packaging-manuals/copyright-format/1.0/
> debconf-i18n/copyright: 1. Redistributions of source code must retain the above copyright
> debconf-i18n/copyright: 2. Redistributions in binary form must reproduce the above copyright
Note: If debconf wasn't in the output of the diff command you ran, choose a string from a different directory name from the output.

Run a "long-output" ls command of the /usr/share/doc directory and filter for debconf to view metadata associated with both the debconf and debconf-il8n` directories.

ls -l /usr/share/doc/ | grep debconf
The output should include something like this (note the -> characters that identify symbolic link relationships):

drwxr-xr-x 2 root root  5 May 18 12:57 debconf
lrwxrwxrwx 1 root root  7 Apr 12  2024 debconf-i18n -> debconf
You've successfully used grep (and other tools) to find and identify system resources and assess their object characteristics.
