## URL:   https://cted.cybbh.io/tech-college/pns/public/pns/latest/guides/bash_sg.html

## Linux Commands URL: https://ss64.com/bash/   

## Extra https://linuxhandbook.com/find-exec-command/

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
```

## find [path] [arguments] -exec [command] {} \; 
```
    [command] is what you want to execute over results given by the find command.
    {} is a placeholder that is used to hold results given by the find command.
    \; says that for each found result, the [command] is executed. You need to escape the ; here and hence \;.
```

##sudo !! = runs last command in root



  


```

##
