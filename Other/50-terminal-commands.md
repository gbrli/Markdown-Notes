# 50 Terminal Commands

## Basic Commands

`whoami` returns name of logged user.

`man` is a manual and will explain other commands. ex `man whomai`, or even `man man`. press `q` or `^C` to exit screen.

`clear` will clear the terminal window. `clear -x` will leave the history on top to scroll up.

`pwd` returns the current working directory, meaning where you are.

`ls` will list the contents of a folder. `ls -a` will also list in hidden files, and `ls -la` will list do the same in long format.

`cd` will change the directory in use. `cd ..` goes back to parent directory. `cd ~` goes back to the username home folder.

## Directories

`mkdir` will create a folder.

* `mkdir winter spring summer fall` creates multiple folders.
* `mkdir winter/seeds` creates seeds inside winter.
* `makedir -p spring/seeds/lettuce` will create all the parent folders if they are missing.
* `makedir ~base` will create folder at the root.

`touch` creates a file `touch index.html`. Can be used to create multiple files as well.

`rmdir` will only remove empty directories

`rm` will remove directories and files both.

* `rm -r foldername` will also delete files inside a folder.
* `rm -v filename` will give feedback of what was deleted.
* `rm -i` will ask for confirmation before deletion.

`open` will open files in the current directory.

`mv` will rename something if it's the same file format or move it inside a folder.

* `mv testa.txt test.txt` will rename because it's two files.
* `mv test.txt foldername` will place the text file in the folder.

`cp` copies files or directories.

* `cp apple test_apple` copies the first file into a second one.
* `cp -r fruits frutta` recursive flag allows to copy the entire fruits folder into a frutta folder.

`head` and `tail` return the first or the last 10 lines of file. `tail file.txt -n 20` will return the last 20 lines. `tales file.log -f` will keep printing lines being added to a file, useful for system log files.

`date` will print the current date.

## Redirecting output to a text file

The characters `>` and `>>` can be used to write to files.

* `date > file.txt` will place the output of the date command inside file.txt and overwrite everything else inside it.
* `date >> file.txt` will add the date without erasing prior contents.
* `cat` prints a file's contents. With multiple files, it concatenates them, and it can be outputted to a new file. `cat first.txt second.txt > newfile.txt`.
* `echo words` will print in the terminal. With `> file.txt` it will create the file and redirect the output in it.

`less` will open a file like `man` describes commands, without cluttering the terminal screen.

`wc` means word count. It returns the number of lines, words and bytes are in a file.

## Piping output to commands

The pipe character `|` allows to send a command to another one.

* `ls -al | wc` will show regular and hidden files in a list format and then pipe the output to word count, which will return the word count of the entire list.
* `ls -al | wc > output.txt` will create a text file with the word count.
* `sort` will return the contents of a file and sort them alphabetically. `cat first.txt second.txt | sort > new.txt` will concatenate two files, sort them, then copy the contents in a new text file.
* `uniq` returns unique values and omits duplicates, but they have to be adjacent or everything will be considered unique. Piping it with sort solves the problem: `sort file.txt | uniq`

## Expansions

Certain characters will be interpreted by the shell and expanded. They can be used with commands.

* `$PATH` and `$USER`
* `*.???` return everything (`*` means all) with a 3-char file extension.
* `echo F*` will return files that start with a capital F.
* `echo {a,b,c}.txt` will return a.txt, b.txt and c.txt. So, `touch app.{js,html,css,py}` will create 4 files with the same name and different extensions.
* `mkdir {1..99}` will create 99 folders with the numbers as their name.

`diff` will return the difference between two files.

## Searching

`find .` will return all files in the current directory.

* `find Roba -name` '*.js' will return all JS files with any name in the Roba folder.
* `find . -type d` will return all directories in current folder.
* `find . -name 'E*' -or 'F*'` will return files in current directory whose name starts with E or F.

`Grep` will look for matches using regular expressions. It is incredibly powerful because of regex and a whole topic on its own.

* `grep <html> file.html`
* `grep -r "word" .` the recursive flag make it search in all folders and files for word.

## Disk and Processes

`du` stands for disk usage and will return the disk usage of files. `du -h` will return human-readable sizes.

`df` will display free disk space. `df -h Desktop`

`history` will return the recent command history in the terminal. It can be piped to look within the history. `history | grep "banana"`

`ps` will return all user-initiated process and can be piped to grep.

`top` will return a list of processes using the CPU at the moment. `top -o mem` will return them sorted by current memory usage.

`kill 12345` will kill an active process. The PID (process ID) is displayed with ps or top. If it doesn't work, you can try `kill -15 12345`, and the more brutal `kill -9 12345`.

`killall -9 node` will brutally kill all processes with the name node.

`process &` the ampersand will make a process run in the background. They can be checked with `jobs`, and `fg` will bring it back to the foreground. `bg` also exists.

## Zip and Archive

`gzip` will zip a file to .gz format. It will delete the original file unless you do the following `gzip -k filename.txt`. Unzipping can be done with `unzip`.

`tar -cf archive.tar file1 file2` will create a .tar archive file. `tar -xf archive.tar` will unarchive in current directory.

## Custom Commands and More

`nano file.txt` will launch a text editor within the terminal.

`alias` will list user-created terminal commands.

* To create them, they need to be inserted with the `nano` editor into a specific file: `nano ~/.zshrc`. Inside the file, the alias command declares a new one, such as `alias ll='ls -la'`. Once this is declared, refresh the file with `source ~/.zshrc` and it will be active.
* If they are not saved onto that file, they will only be valid for the current terminal session and then disappear.
* The alias declaration used with single quotes `'` will make the command valid in any directory. If double quotes `"` are used instead, the new command will only be valid in the initial directory.

`xargs` is used in conjunction with piping `|` to transfer arguments to the second command.

* If a file contains a list of other files, this will not work: `cat text.txt | rm'`.
* Using xargs will instead pass the output of `cat text.txt` to the `rm` command: `cat text.txt | xargs rm`. This will delete the files in the current directory that were listed in text inside text.txt.
* `xargs` turns standard input into a list of arguments.

`ln` creates a soft or hard link between files. Linked files will share their contents.

* `ln -s 1.txt soft.txt` will link the two files together by having soft.txt point to 1.txt. If the original files gets deleted, the soft linked files will remain but it will be empty.
* `ln 1.txt hard.txt will have both files point to the same place in the computer memory, so if the original file is deleted, the new one will remain.

## Admin Commands

`who` displays all users logged into the machine.

`su` means substitute user and will enable to enter as a different user. `su username` will them ask for the user password. `exit` will return to the initial user logged in.

`sudo` means super user do. It is used before a command line to act as a root user and will require the user password to run.

`passwd` will change the user password. It can be done with other users as `sudo passwd username`

`chown` changes the ownership of a directory, and it requires root permission. `sudo chown -R newuser directory/` with the recursive flag, the ownership of the directory as well as all the files on the inside will change.

Permissions are stored as a 10-digit string. The first  character is the file type, such as `d` for directory, `l` for soft links, and `-` for regular files. The other 9 characters are split into three categories: owner, group and world. Each group is split into 3: read permission, write permission, execute permission. The value can be r (read), w (write), x (execute), - (no permissions). `rw-------` will only give the owner permission to read and write.

`chmod` will change permissions.

Source: <https://www.youtube.com/watch?v=ZtqBQ68cfJc>
