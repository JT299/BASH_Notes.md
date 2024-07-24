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

{} = placeholder
\; = everything you find 
+ = command is executed only once
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

## awk:   Find and Replace text, database sort/validate/index.
```
awk -F: '{print $1}'         displays 1st field delimited by a ":"
awk '{print $2}'             displays 2nd field, delimited automatically by space
awk '{print $0}'             displays all string data that matches

awk -F: '($3 == 0) {print $1}' /etc/passwd
(if field 3 is equal to 0, print field 1)   displays 1st field (username) IF the 3rd field (UID) is equal to "0"

awk '{print $NF}'           displays only the last field of every lineFind and Replace text, database sort/validate/index.

awk -v = calling a variable

EX: awk -F: 'BEGIN {OFS="@"} {print $1, $3}' fakepasswrd.txt
OFS = Out Field seperator

cat fakepasswd.txt | awk -F: 'BEGIN {OFS=":"} {print $1,$3}' fakepasswd.txt

####
EX: cat /etc/passwd | awk -F: '($3 >= 150){print $0}'

nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
student:x:1001:1001::/home/student:/bin/bash

####
EX: cat fakepasswd.txt | awk -F: '($3 >= 150){print $1, $6, $3}'

 nobody /nonexistent 65534
ubuntu /home/ubuntu 1000
student /home/student 1001

####
EX:  awk -F: '($7 == "/usr/sbin/nologin"){print $1, $6, $3}' fakepasswd.txt
```

## Sort: Sort text files. Sort, merge, or compare all the lines from the files given (or standard input.)
```
sort                sorts content according to position on the ASCII table
sort -n             sorts content numerically
sort -u             sorts content uniqely
sort -nr            sorts content numerically reversed
sort -t +
sort -k 2,4         sorts 1st by content in the 2nd column, then by content in the 4th column
(column = -k // -k 2,4 == sorting by the second and fourth column)

EX: awk -F: '{print $3}' fakepasswd.txt | sort
(command before sort, has to be piped)

cat fakepasswd.txt | sort -t : -k 7(seperator by :)
```

## BASH PRactice DAY2
```
EX6:
Activity:

Write a basic bash script that greps ONLY the IP addresses in the text file provided (named StoryHiddenIPs in the current directory); sort them uniquely by number of times they appear.

A:
cat StoryHiddenIPs | grep -E -o "([0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3})" | sort -n | uniq -c | sort -nr

########
Q7:
Activity:

    Using ONLY the awk command, write a BASH one-liner script that extracts ONLY the names of all the system and user accounts that are not UIDs 0-3.
    Only display those that use /bin/bash as their default shell.
    The input file is named $HOME/passwd and is located in the current directory.
    Output the results to a file called $HOME/SED/names.txt

Tip: awk can use conditional statements, e.g. print only the line in /etc/passwd that has "root" as its first field.

A:
cat $HOME/passwd | awk -F: '($3 > 3)' | awk -F: '($7 == "/bin/bash"){print $1}' > $HOME/SED/names.txt

OR

awk -F '($3 != "0" && $3 != "1" && $3 != "2" && != "3") {print $0}' -/passwd | awk -F: '($7 == "/bin/bash")' | awk -F: '{print $1}' > -/SED/names.txt
```

## Sed: 
```
SED is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline).
While in some ways similar to an editor which permits scripted edits, SED works by making only one pass over the input(s), and is consequently more efficient. But it is SED’s ability to filter text in a pipeline which particularly distinguishes it from other types of editors.

sed '/.dll/{x;p;p;p;x}' -i document.txt
    directly alters document.txt by adding 3 empty lines before the designated regex (.dll)

sed '/stuff/G;/stuff/G' -i document.txt
    directly alters document.txt by adding 2 empty lines after the designated regex (stuff)

sed -i -e 's/ANCHOVIES/SAUSAGE/g' pizaster.htm
            replaces every instance of "ANCHOVIES" with "SAUSAGE" on pizaster.htm

sed -i -e 's/ANCHOVIES//g' pizaster.htm
            removes every instance of "ANCHOVIES" on pizaster.htm

sed -i '/^#/d' /etc/hosts.allow
            removes all lines starting with "#" from file /etc/hosts.allow

sed -e == -e means script
/g = globally
/s = switch
```

## Command Substitution:
```
A=$(Command)            A=$(cat /etc/passwd)
`Command`               `cat /etc/passwd`
```

## Aliases:
```
alias rm='rm -i'                    creates alias to confirm removal
alias vim='nano'                    creates an alias for `nano'
alias gedit='nano'                  "
alias vi='nano'                     "
alias x='cat etc/passwd'            creates an alias for Command: cat/etc/passwd
alias y=$(cat /etc/shadow)          " cat /etc/shadow
alias ls='ls -al'                   creates an alias causing 'ls -al' to be run when 'ls' is used
\ls                                 negates the alias function, so we can run 'ls' without '-al'
alias -p                            view all aliases set (local and global)
unalias ls                          unaliases ls so it no longer resolves to 'ls -al'
```
## BASH PRACTICE:
```
Q8:

    Find all dmesg kernel messages that contain CPU or BIOS (uppercase) in the string, but not usable or reserved (case-insensitive)
    Print only the msg itself, omitting the bracketed numerical expressions ie: [1.132775]

A:
dmesg | grep -E 'CPU|BIOS' | grep -E -i -v 'usable|reserved' | cut -d] -f2-

#################
Q9:

    Write a Bash script using "Command Substitution" to replace all passwords, using openssl, from the file $HOME/PASS/shadow.txt with the MD5 encrypted password: Password1234, with salt: bad4u
    Output of this command should go to the screen/standard output.
    You are not limited to a particular command, however you must use openssl. Type man openssl passwd for more information.

A:
A=$(openssl passwd -1 -salt bad4u Password1234)
awk -F: -v "awk_var=$A" 'BEGIN {OFS=":"} {$2=awk_var} {print $0}' $HOME/PASS/shadow.txt


##############
Q10:
Using ONLY sed, write all lines from $HOME/passwd into $HOME/PASS/passwd.txt that do not end with either /bin/sh or /bin/false.

A:
sed -e '/\/bin\/false/d' -e '/\/bin\/sh/d' $HOME/passwd > $HOME/PASS/passwd.txt
```

## Day 3:

## tar
```
Store, list or extract files in an archive (originally on tape - Tape ARchiver).

tar -czf   ==

z = This option tells tar to read or write archives through gzip, allowing tar to directly operate on several kinds of compressed archives transparently. See section (gzip)

f = tar will use the file archive as the tar archive it performs operations on, rather than tar’s compilation dependent default. See section The

c = create 
```
## Expressions:
```
#!bin/bash
A=120
B=20
expr $A - $B
```

EX: IF ELSE statement
```
#!/bin/bash

contents=$(cat simple.txt)
if [[ $contents == "tacos" ]]; then
        echo "are good on tuesdays"
elif [[ $contents == "costco is amazing" ]]' then
        echo "and will save you money"
elif [[ $contents == "chicken bake" ]]; then
        echo "tasty but will make you fail ht/wt"
else
        echo "no tax at commissary"
fi
```
## Variable subitution:
```
#!/bin/bash
A=him
echo The story of Robert who os $A
echo I am $A
echo I will remain $A
```

## BASH Practice Question 11: 
```


Activity:

    Using find, find all files under the $HOME directory with a .bin extension ONLY.
    Once the file(s) and their path(s) have been found, remove the file name from the absolute path output.
    Ensure there is no trailing / at the end of the directory path when outputting to standard output.
    You may need to sort the output depending on the command(s) you use.

Tip: For stripping the filename out of the output, there are different ways that this can be accomplished based on what you have learned so far.

    Utilizing -printf options on find.
    Utilizing awk to manipulate the fields. This may leave the trailing / if you don't take that into account.
    Utilizing the rev and cut commands creatively.


A:
find $HOME -name "*.bin" 2>/dev/null | rev | cut -d/ -f2- | rev | sort -u
```

## BASH Practice Question 12: 
```


Activity:

    Write a script which will copy the last entry/line in the passwd-like file specified by the $1 positional parameter
    Modify the copied line to change:
        User name to the value specified by $2 positional parameter
        Used id and group id to the value specified by $3 positional parameter
        Home directory to a directory matching the user name specified by $2 positional parameter under the /home directory
        The default shell to `/bin/bash'
    Append the modified line to the end of the file

Tip: awk provides the simplest method for completing this activity. Refer back to your notes on "09 - BASH Activity" if you are in need of starting point on this activity.

Note: The contents of the passwd-like file will be randomly generated on each submission. It is intended to read the last line once and store it in a variable.

To read more on Positional Parameters, go to the following resource:

    https://www.gnu.org/software/bash/manual/bash.html#Positional-Parameters

To read more on the Passwd file format, go to the following resource:

    man passwd.5


A:
#!/bin/bash

file=$1
UN=$2
id=$3

tail -1 $file | awk -F: -v "uname=$UN" -v "ident=$id" 'BEGIN {OFS=":"} {$1=uname}{$3=ident}{$4=ident}{$6="/home/"uname}{$7="/bin/bash"}{print $0}' >> $file
```
## Bash Question 13:
```

    Find all executable files under the following four directories:
        /bin
        /sbin
        /usr/bin
        /usr/sbin
    Sort the filenames with absolute path, and get the md5sum of the 10th file from the top of the list.

Tip: In the below example, you can see the different uses of md5sum. While not wrong, the first command is hashing the string output of the the find command. In the second, md5sum is hashing the file contents of the given file, which is what is intended for this activity. You can also tell the second method hashed the file as the file name is listed in the hash output; the first only lists a hyphen indicating a string was hashed. For this activity, to provide md5sum with the 10th file of the sorted output, it is recommended to use Command Subtitution.

A:
A=$(find /bin /sbin /usr/bin /usr/sbin -type f -executable | sort | head | tail -1)
md5sum $A | cut -d' ' -f1
```

## REVIEW:
```
grep -v = invert search

tar -czf

-maxdepth

wc = word count
wc -l = line count

touch -d or -c = change the date of a file

*** Command subsitution / Variable Subsitution ***

sed = swap out things in a file

sort -options

ls -1
ls -l
```



