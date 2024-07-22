## URL:   https://cted.cybbh.io/tech-college/pns/public/pns/latest/guides/bash_sg.html

## Linux Commands URL: https://ss64.com/bash/   

## Extra https://linuxhandbook.com/find-exec-command/

## -printf URL help: https://phoenixnap.com/kb/bash-printf

## Single vs Double Brackets help URL: https://www.baeldung.com/linux/bash-single-vs-double-brackets

## Bash Scripts: nano <name>.sh

## Linux Commmands:
```
man = 'looks at man pages'

touch / mkfile = makes new file
  -t = make a certain time

mkdir -p  = makes a parent directory

umask = checks permissions

chmod = changes permission on a file

rm = removes a file
  -rf = forces to remove

rmdir = removes directory

ls = long listing of directory
  -lisa = 
  -1 = -'one' = one per line

pwd = present working directory / see where you are at

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

##
