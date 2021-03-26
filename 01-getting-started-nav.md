# Getting Started with Nav

## Basic Navigation Commands
List of basic commands on a terminal or command-line.
- `ls` -- list the current directory contents
- `pwd` -- output the current directory path
- `cd` -- change directory path
- `open` -- opens the file on the ui

Lets try it out!

1. List your current directory path.

Example:
```
❯ pwd
/Users/jyang
```
2. Now list everyting in that path. 
```
❯ ls
Applications Documents    Library      Music        Public       go           pod.yaml
Desktop      Downloads    Movies       Pictures     github       p_creds
```
If you add the `-l` parameter specific to `ls` it will organize the output into a list.
```
❯ ls -l
total 16
drwx------@  6 jyang  staff   192 Apr 17  2020 Applications
drwx------@ 14 jyang  staff   448 Mar  3 22:40 Desktop
drwx------@ 27 jyang  staff   864 Mar  3 18:07 Documents
drwx------@ 37 jyang  staff  1184 Mar  1 15:14 Downloads
drwx------@ 77 jyang  staff  2464 Jan 15 20:25 Library
drwx------+  6 jyang  staff   192 Mar 10  2020 Movies
drwx------+  4 jyang  staff   128 Feb  9  2020 Music
drwx------+  6 jyang  staff   192 Sep  4 15:58 Pictures
drwxr-xr-x+  4 jyang  staff   128 Feb  5  2020 Public
lrwxr-xr-x   1 jyang  staff    16 Feb  5  2020 github -> Documents/github
lrwxr-xr-x   1 jyang  staff    12 Feb 14  2020 go -> Documents/go
-rw-------   1 jyang  staff   116 May  5  2020 p_creds
-rw-r--r--   1 jyang  staff   279 Apr 30  2020 pod.yaml
```
3. Now try changing your directory and explore what files exist in each directory. 
```
❯ ls -l
total 595936
drwxr-xr-x    8 jyang  staff        256 May 23  2020 AustinYang Can Delete
-rw-r--r--@   1 jyang  staff      79279 Sep  4 16:06 Photo on 9-4-20 at 4.06 PM #3.jpg
-rw-r--r--@   1 jyang  staff     131095 Sep  7 13:49 Photo on 9-7-20 at 1.49 PM #2.jpg
-rw-r--r--@   1 jyang  staff    1931339 Mar 20  2020 Screen Recording 2020-03-20 at 6.24.31 PM.mov
-rw-r--r--@   1 jyang  staff  287550206 Mar 20  2020 Screen Recording 2020-03-20 at 6.24.55 PM.mov
-rw-r--r--@   1 jyang  staff      23101 Feb 10  2020 Screen Shot 2020-02-10 at 4.23.17 PM.png
-rw-r--r--@   1 jyang  staff      22961 Mar  3  2020 Screen Shot 2020-03-03 at 11.01.13 PM.png
-rw-r--r--@   1 jyang  staff      22099 Mar  8  2020 Screen Shot 2020-03-08 at 11.16.40 PM.png
drwxrwxrwx  317 jyang  staff      10144 Jun 27  2020 kongandlila
-rw-r--r--@   1 jyang  staff        341 Mar  4 23:03 test.yaml
```
4. Then print out your path to see the difference.
```
❯ pwd
/Users/jyang/Desktop
```
5. Try to go back to where you started.
```
❯ pwd
/Users/jyang/Desktop
❯ cd /Users/jyang
❯ pwd
/Users/jyang
```
Sometimes it takes longer to navigate back one directory above or to go back to `$HOME`. Here are some technques to master navagation. 

Example 1 -- great to use when you're wanting to go back just a few directory/directories.
```
❯ pwd
/Users/jyang/Desktop
❯ cd ..
❯ pwd
/Users/jyang
❯ cd ../..
❯ pwd
/
```
Example 2 -- good to use when you want to go back to your home directory.
```
❯ pwd
/
❯ cd
❯ pwd
/Users/jyang
```
Example 3 -- best practice to use `~/` which allows you to start at the beginning of your home directory. Sometimes some linux/unix based operating systems don't understand tilda `~`.
```
❯ pwd
/Users/jyang/Desktop/kongandlila
❯ cd ~/
❯ pwd
/Users/jyang
```
Example 4 -- best practice to use in your script so that you know exactly where you're starting. 
```
❯ pwd
/Users/jyang/Desktop
❯ cd $HOME
❯ pwd
/Users/jyang
```

### Summery
These commands will benefit you in the long run as you become more familiar with the command-line. Computers with a GUI (graphic user interface) carry a lot of work and consumes a lot of resources; that being compute, memory and storage. Using the command-line is very accurate and very powerful. You can manipulate data (files or contents in a file) on a very largers scale.

__Bonus__ -- `open` a file or directory. 

### Just me rambling on... for context.

Businesses want to run efficently. In theory having a server with GUI consumes more resources and time. Just think about it, although graphics may consume more compute, memory and storage its more work for a computer, more electricity to keep it thinking and more electricity means more money. When you have hundrends and even thousands of servers with these extra GUI the all stack up.

One of the perks of a command-line on servers like Linux/Unix is the ability to run scripts. Scripts are kind of like a programming language but different in that they use command-line and system instructions. You can write them in a file from top to bottom and it will run the directions from top to bottom.

On Windows Servers, especially older operating systems, can run on scripts (often in the form of a file  called .exe) but are notorious for their GUI which is fatiguing sometimes because you have to constantly interact with it and if the connection is poor/slow/unresponsive using it becomes frustrating. I will say Windows Server do manage users and access a lot better but for development they are a nightmare.

> This managing tool/application is called Active Directory; AD for short. 

Knowing how to navigate on the command-line will help you become a better coder (aka programmer, developer). Some of the tools you will commonely use to help you stay in sync with your team is heavly command-line based. 


## Basic System Administrator Commands && Permissions
- `whoami` -- output user name
- `who` -- outouts who is currently on the computer as a user
- `id` -- outputs user information
- `groups` -- outputs group associated with user
- `chmod` -- change access to a file or directory
- `chown` -- change owner to a file or directory
- `df` -- output disk/storage capacity
- `date` -- outout date and computer time-zone
- `time` -- output how long computer has been runnning

## Basic Troubleshooting Commands && Troubleshooting Methods w/ OCI
- `man` -- every command has a manual/instructions
- `ps` -- list process status
- `find` -- outputs every possible path
- `which` -- locates the location of a command 
- `uname` -- outputs computer info
- `nslookup` -- looks for computer names via ip address and vice-versa
- `host` -- looks up dns name related to a ip address

## Advance Commands
- `curl` -- transfer data from or to another computer or vice-versa
- `printenv` -- outputs command-line environment variable
- `grep` -- file pattern searcher
- `mount` 

## Understand Basic Networking

## Create simple script

## Create simple HTML

## Understand development process

## Understand DevOps

## Understand Virtualization

## Understand Containerization

## Understand Datacenters and Cloud (AWS|AZURE|GCP|OCEAN DIGITAL)

## Understand Kubernetes