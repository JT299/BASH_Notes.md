## URL:   https://cted.cybbh.io/tech-college/pns/public/pns/latest/guides/bash_sg.html

## Linux Commands URL: https://ss64.com/bash/   

## Extra https://linuxhandbook.com/find-exec-command/

## -printf URL help: https://phoenixnap.com/kb/bash-printf

## Single vs Double Brackets help URL: https://www.baeldung.com/linux/bash-single-vs-double-brackets

## URL: http://10.50.26.116

## Bash Scripts: nano <name>.sh

## Linux Commmands: DAY 1
```
man = 'looks at man pages'

touch / mkfile = makes new file
  -t = make a certain time

mkdir -p  = makes a parent directory

umask = checks permissions

chmod = changes permission on a file ps -u Jim 		IDs processes use by user: Jim
 ps --forest 		show complete process tree with parent child relationships
 ps -u Jim –-forest 	show for user: Jim only
 ps u U Jim –-forest 	owned by user: Jim
 ps aux 		a == shows all procs running on system
 			u == users running the proc
 			x == CMDs that ran the procs.

rm = removes a file
  -rf = forces to remove

rmdir = removes directory

ls = long listing of directory
  -lisa = 
  -1 = -'one' = one per line

pwd = present working directory / see where you are atls -l $HOME/CUT | cut -d: -f2 | cut -d' ' -f2 | cut -d. -f1-2 -s > $HOME/CUT/names

cp <source> <dest> = copys a file

cat = views contect of file
more =
less =
head = 10 first lines
   head -5 = gives the first 5 lines
tail = 10 last lines
   tail -5 = gives last 5 lines

find = find 
  -name = case sentivitity //EX: find - name \*.txt == wildcard to find all txt files
  -iname = case insentivitive
  -inum = inode number
  -size = ex: find -size -1G = less than 1g /// -size +1G = more than 1G
  -group
  -gid = find by group id //EX: cat /etc/passwd | grep student
  -uid = user id
  -maxdepth = tells how many directories to deep into
  -type d = finds directorys ///EX: find / -type d
    f = file
  ** Good to know **
  -atime 3 = accessed in the last 3 days
  -ctime 3 = changed in the last 3 days
  -mtime 3 = modified in the last 3 days
  -amin 180 = accessed in the last 3 hours
    cmin = changed 
    mmin = modified

  $HOME -mtime 0 = home directory
  /etc/ -mtime 0 = looks at home directory

**********            *******
find / -perm /4000 -uid 0 -ls 2>/dev/null
  -perm = finds permissions
  2>/dev/null = error statments go to the to null

find /var/log -iname *.log 2>/dev/null -printf "%i %f\n"
  -printf = converts, formates and writes its argument parameters to standard output.

find / -inum 38 2>/dev/null
     = finds any inode of 38
```

## find [path] [arguments] -exec [command] {} \; 
```
    [command] is what you want to execute over results given by the find command.
    {} is a placeholder that is used to hold results given by the find command.
    \; says that for each found result, the [command] is executed. You need to escape the ; here and hence \;.
```

## sudo !! = runs last command in root

## GREP
```
Used for searching and matching text patterns in files contained in the regular expressions.

grep -c                 counts number of lines that match
grep -r ; grep -R       recursive
grep -f                 files only
grep -E                 regular expressions (GNU)
    or egrep 
grep -o                 displays ONLY matches of regex / not whole line
grep -i                 case-insensitive match
grep -l                 displays only file name (full path) of matching regex
grep -C#                in context of match (# of lines before and after)
grep -A#                displays # of lines after matching regex
grep -B#                displays # of line before matching regex
grep -P                 uses Pearl regular expressions (non-GNU)
grep ""                 shell quoting (BASH interpretable)
grep ''                 shell quoting (NOT BASH interpretable)
grep -v                 invert match
grep -n                 print line number with output lines

EX: cat fakepasswd.txt | grep /bin/bash == displays lines that contain /bin/bash in fakepasswd.txt

EX: egrep "student|root|bob" fakepasswd.txt = display anylines that contain "student" "root" or "bob"

EX: cat fakepasswd.txt | grep -v /bin/bash
    === displays lines that DO NOT contain /bin/bash 
```
## Brace Expansion
```
mkdir cosc11{23,45,67}
     == creates directories cosc23, cosc45, cosc67
```

## CLASS PRACTICE Brace Expansions:
```
1:
Brace expansion is a mechanism by which arbitrary strings may be generated, for commands that will take multiple arguements. For the below examples, the first example is equivalent to the second command.

$ mkdir /var/log/{auth,syslog,dmesg}_log

Results in

$ mkdir /var/log/auth_log /var/log/syslog_log /var/log/dmesg_log

Activity: Using Brace-Expansion, create the following directories within the $HOME directory:

    1123
    1134
    1145
    1156

To read more on Brace Expansion, go to the following resource:

mkdir $HOME/{1123,1134,1145,1156}

or

mkdir $HOME 11{23,34,45,56}


Q2:


As we learned, the following example would create five files with one command.

touch file1.txt file2.txt file3.txt passwd.txt shadow.txt

But, with Brace Expansion it can be shortened to the following.

touch file{1..3}.txt passwd.txt shadow.txt

Activity:

Use Brace-Expansion to create the following files within the $HOME/1123 directory. You may need to create the $HOME/1123 directory. Make the following files, but utilze Brace Expansion to make all nine files with one touch command.

Files to create:

    1.txt
    2.txt
    3.txt
    4.txt
    5.txt
    6~.txt
    7~.txt
    8~.txt
    9~.txt

mkdir $HOME/1123
touch $HOME/1123/{1,2,3,4,5,6~,7~,8~,9~}.txt

Q3:
Activity:

Using the find command, list all files in $HOME/1123 that end in .txt.

Be aware that if you use Pattern Matching to locate the files you may have unintended results based on if you use quotes around the pattern or not. If you do not quote the pattern, the Bash shell interprets the pattern. If you quote the pattern, it is passed to the command for it to interpret. You can have a properly functioning command, yet unintended output, based on which of these two gets to interpret the pattern.

find $HOME/1123 -name \*.txt

or

find $HOME/1123/ -type f *.txt

Q4:


Challenge Activity:

List all files in $HOME/1123 that end in .txt. Omit the files containing a tilde (~) character.

While this activity can be accomplished with only find, it can also be combined with grep as well.


find $HOME/1123/ -name \*.txt | grep -v ~.txt

or

find $HOME/1123/ -name "*.txt" | grep -v "~"
```
## kill / pkill 
```
 ps -u Jim 		IDs processes use by user: Jim
 ps --forest 		show complete process tree with parent child relationships
 ps -u Jim –-forest 	show for user: Jim only
 ps u U Jim –-forest 	owned by user: Jim
 ps aux 		a == shows all procs running on system
 			u == users running the proc
 			x == CMDs that ran the procs.
```

## Cut
```
cut line parts from specified files or piped data and print the result to standard output



cut -d: -f1         displays only portion of line before 1st instance of delimiter ``:''
cut -d: -f1-        " and any following strings up to the very next instance ``:''
cut -d: -f1- -s     " " but don’t print any lines not containing delimiter ``:''
cut -f3             displays only the 3rd field delimited by space
cut -f2-4           displays only fields 2 through 4 delimited by space
cut -c3-10          displays only the 3rd through 10th characters of each line

-d: = dilimeter 

NOTE: Tabs are counted as single spaces on a line; both are counted as single characters

EX:: cat fakepasswd.txt | cut -d: -f1 
EX:: cat fakepasswd.txt | cut -d: -f1 -s
    -s \= at the end is for string
```

## Command Chaining Operators:
```
&   --Sends process to background (so we can run multiple process parallel)
;   --Run multiple commands in one run, sequentially.
 \  --To type larger command in multiple lines
&&  --Logical AND operator
||  --Logical OR operator
!   --NOT operator
|   -- PIPE operator
{}  --Command combination operator.
    [ -f 99.txt ] || { echo " does not exist"; touch 99.txt; }
()  --Precedence operator = looks at it first
>   creates a new file or overwrites it if one exsists
>>  appends a file or creates if it does not exsists
```

## 02 BASH ACTIVITY:
```
Q1:


Activity:

Copy all files in the $HOME/1123 directory, that end in ".txt", and omit files containing a tilde "~" character, to directory $HOME/CUT.

Use only the find and cp commands. You will need to utilize the -exec option on find to accomplish this activity.

The find command uses BOOLEAN "!" to designate that it does not want to find any files or directories that follows.


find $HOME/1123 -type f ! -name "*~*" -name "*.txt" -exec cp {} $HOME/CUT \;

OR

find $HOME/1123 -name "*.txt" ! -name "*~*" -exec cp {} $HOME/CUT \;

Q2:


Activity:

Using ONLY the find command, find all empty files/directories in directory /var and print out ONLY the filename (not absolute path), and the inode number, separated by newlines.

Tip: When using the man pages, it is better to focus your search then to visually scan 1000+ lines of text. Combining the output with the grep command, possibly with its -A, -B, or -C options, can help drive context driven searches of those manual pages.

Example Output

123 file1
456 file2
789 file3

A:
find /var/ -empty -printf "%i %f\n"


  *** -empty = searches for empty files
  *** %i = inode number
  *** %f = file name

Q3:



Activity:

Using ONLY the find command, find all files on the system with inode 4026532575 and print only the filename to the screen, not the absolute path to the file, separating each filename with a newline. Ensure unneeded output is not visible.

Tip: The above inode is specific to this CTFd question and might not be in use on your Linux Opstation. Instead, you can test your command on your Linux OpStation against inode 999.


A:
find / -inum 4026532575 -printf "%f\n"

OR

find / -inum 4026532575 -priintf "%f\n" 2>/dev/null


Q4:
Activity:

    Using only the ls -l and cut Commands, write a BASH script that shows all filenames with extensions ie: 1.txt, etc., but no directories, in $HOME/CUT.
    Write those to a text file called names in $HOME/CUT directory.
    Omit the names filename from your output.

NOTE: The output should only be the file names with no additional information. Additionally, your code will be executed twice. This is to ensure you have taken into account how file redirection and command execution works.

A:
ls -l $HOME/CUT | cut -d: -f2 | cut -d' ' -f2 | cut -d. -f1-2 -s > $HOME/CUT/names

or

ls -l | cut -d' ' -f9 -s | cut -d. -f1-2 -s
```

## DAY 2 

## 
