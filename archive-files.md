You can use tar to create a backup of the /usr/share/doc directory. The archive you are required to create should not be compressed, and should be stored in your home directory as ~/doc.tar, Use **tar -c** to create, and **-f** to specify the backup file, and then the path to the directory. First check the size of the directory using **du -sh** /usr/share/doc, this should be 30M, then run the backup and list the size of the backup file created, which should be 21M. The file is not compressed; however, more efficient use of the storage is maintained as it is a single file rather than many files:

Check the size of the directory:
> du -sh /usr/share/doc
Create the archive file:
> tar -cf ~/doc.tar /usr/share/doc
List the archived file:
> ls -lh ~/doc.tar

*du = estimate file space usage
-s = summarize
-h = human readable
*tar = archving utility
-c = create
-f = specify the file, usually the action command with f after - tar -cf path
-t = list the contents of the archived file
-x = extract files from an archive

List the contents of the archived file:
> tar -tf ~/doc.tar

Extract the contents of the archived file:
> tar -xf ~/doc.tar
By default the restore will be to the working directory.
Verify the restore:
> tree ~/usr

**Restoring a single file**
Find and delete a file:
> find /usr/share/doc -type f -name "\*.pdf"
If one file is returned:
> sudo /usr/share/doc -type f -name "\*.pdf" -delete
Extract the required file from the archive back to its correct location:
> sudo tar -C / -xf \<archivefilename> \<filepath>

<img width="1444" height="200" alt="image" src="https://github.com/user-attachments/assets/c08577f9-0032-42e9-8f4b-2b0c96d107d9" />

Create an archive with compression:
-z = make a gzip compression
file extension = tgz or tar.gz
> tar -czf ~/doc.tar.gz /usr/share/doc
Verify:
> ls -lh ~/doc.tar*

Extreme compression:
> tar cJf \<archivepath>.xz \<pathofdirectory>
This takes longer, but can be ran in the background by redirecting the output to /dev/null or another file:
> tar -cJf ~/doc.tar.xz /usr/share/doc &> /dev/null &
A done message will display when you next press enter.

<img width="1462" height="284" alt="image" src="https://github.com/user-attachments/assets/e3e4ab1f-6f1b-4124-9aa8-7e3408583218" />





