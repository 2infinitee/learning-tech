# Getting Started with Computers

## Basic Read/Write Commands
- `mkdir` -- creates a directory
- `rm` -- deletes files or directory paths **(use extra caution)**
- `touch` -- create a file
- `vim` -- command-line text editor
- `cat` -- concatenate and print contents of a file
- `echo` -- writes to stdout
- `less` -- allows you to read a file either at the bottom or top 
- `cp` -- copy
- `mv` -- move/rename

Lets get started!

1. Make a directory using `mkdir` and change to that directory. Directories are like folders on Windows but the correct term is directory. 
    ```
    ❯ pwd
    /Users/jyang
    ❯ ls -l
    total 16
    drwx------@  6 jyang  staff   192 Apr 17  2020 Applications
    drwx------@ 14 jyang  staff   448 Mar  4 23:03 Desktop
    drwx------@ 27 jyang  staff   864 Mar  3 18:07 Documents
    drwx------@ 37 jyang  staff  1184 Mar  1 15:14 Downloads
    drwx------@ 77 jyang  staff  2464 Jan 15 20:25 Library
    drwx------+  6 jyang  staff   192 Mar 10  2020 Movies
    drwx------+  4 jyang  staff   128 Feb  9  2020 Music
    drwx------+  6 jyang  staff   192 Sep  4  2020 Pictures
    drwxr-xr-x+  4 jyang  staff   128 Feb  5  2020 Public
    lrwxr-xr-x   1 jyang  staff    16 Feb  5  2020 github -> Documents/github
    lrwxr-xr-x   1 jyang  staff    12 Feb 14  2020 go -> Documents/go
    -rw-------   1 jyang  staff   116 May  5  2020 p_creds
    -rw-r--r--   1 jyang  staff   279 Apr 30  2020 pod.yaml
    ❯ mkdir justin-test-dir
    ❯ ls -l
    total 16
    drwx------@  6 jyang  staff   192 Apr 17  2020 Applications
    drwx------@ 14 jyang  staff   448 Mar  4 23:03 Desktop
    drwx------@ 27 jyang  staff   864 Mar  3 18:07 Documents
    drwx------@ 37 jyang  staff  1184 Mar  1 15:14 Downloads
    drwx------@ 77 jyang  staff  2464 Jan 15 20:25 Library
    drwx------+  6 jyang  staff   192 Mar 10  2020 Movies
    drwx------+  4 jyang  staff   128 Feb  9  2020 Music
    drwx------+  6 jyang  staff   192 Sep  4  2020 Pictures
    drwxr-xr-x+  4 jyang  staff   128 Feb  5  2020 Public
    lrwxr-xr-x   1 jyang  staff    16 Feb  5  2020 github -> Documents/github
    lrwxr-xr-x   1 jyang  staff    12 Feb 14  2020 go -> Documents/go
    drwxr-xr-x   2 jyang  staff    64 Mar 14 16:36 justin-test-dir
    -rw-------   1 jyang  staff   116 May  5  2020 p_creds
    -rw-r--r--   1 jyang  staff   279 Apr 30  2020 pod.yaml
    ❯ cd justin-test-dir
    ❯ ls -l
    ❯ pwd
    /Users/jyang/justin-test-dir
    ```

    As you can see there is nothing in that directory after creating it. 

2. Make another directory. Now without going into that sub-directory make another sub-directory in that sub-directory.
    ```
    ❯ mkdir 1
    ❯ cd 1
    ❯ pwd
    /Users/jyang/justin-test-dir/1
    ❯ mkdir 2/3
    ❯ ls -l
    total 0
    drwxr-xr-x  3 jyang  staff  96 Mar 14 16:40 2
    ❯ cd 2
    ❯ ls -l
    total 0
    drwxr-xr-x  2 jyang  staff  64 Mar 14 16:40 3
    ❯ cd 3
    ❯ ls -l
    ❯ pwd
    /Users/jyang/justin-test-dir/1/2/3
    ```
3. Create a file with the `touch` command and one in the deepest sub-directory you just created.
    ```
    ❯ pwd
    /Users/jyang/justin-test-dir/1/2/3
    ❯ touch deep-file.txt
    ❯ ls -l
    total 0
    -rw-r--r--  1 jyang  staff  0 Mar 14 16:46 deep-file.txt
    ```

4. Output the file using `cat` then `less`. Understand their behaviors. `cat` means concatenate (to join). `less` is a newer version of another commnad called `more`.
    ```
    ❯ cat deep-file.txt
    ❯ less deep-file.txt
    ```

    They don't return anything because the file is empty lol.

5. Write to file in the deepest directory with `vim`. Make sure you have a couple of lines.
    ```
    ❯ vim deep-file.txt
    ❯ cat deep-file.txt
    yang
    ❯ less deep-file.txt
    yang
    ```
    You cant see the part where i wrote in "yang" because it takes you into a word editor.
6. Use `cat` to write something to the other file. 
7. Use `cat` and `less` again to output each file content.
8. Use `cp` to copy a file or directory. 
9. Use `mv` to move a file or directory and then rename a file or directory.
8. Now delete one of the files with `rm`.
9. Delete everything you created. __CAUTION DO IT WITH CARE__

### Summery
Becareful of what you write/delete. The smallest change to a file can have a cascading effect. If you alter or delete files mistakenly reverting the change can be very difficult, sometimes impossible. If you're unsure rename the file with a random file extension or move it to another location. 

Lastly, the number 1 rule for every one out there. Know what you're deleting with `rm -rf`. The `/` is called the `root` path which is the main directory for everything on the computer. Deleting this will cause your computer to be wiped out completely. Do not mistaken this with the home directory - a home directory exist per user on the computer. Deleting a home directory will only delete the user's profile and everything on it. 

### Just me rambling on... for context.
For best-practices, you should always backup your files. As you become more and more embeded into technology you will realize that there are tools that some folks never realized exist. One such tool is `git`, which is a version control tool that allows you to save a history of a file at a certain state and be stored on a repository for you the share with other teammembers. Whenever someone makes a update they will __push__ it up to the repository and everytime you go and work on the same project you will make a __pull__ to see if its been changed in any way. Git also keeps track of changes too and if there were any conflicting files that are totally different it will tell you where exactly that is! Neat isn't it?

There is a couple version control tools out there but the main one everyone uses is `git`. `git` is also an open-source project and is free! But don't get confused with GitHub. GitHub is a company that built its own version of `git` on top of the open-source project that allows you to see these __pulls, push, and change conflicts__ through the browser. GitHub also makes it easier to share with teammates as well over the internet.

GitHub on the web is free. The open-source community typically use GitHub to store their projects there for anyone to use. If their repository is public you can download them. You can also make it private and share with select individuals. This is how you can become a technologist and never become too old for the newer generation of technology because you're the one who is keeping up with technology and making it more efficent and autonomous. They say theres only 3% of the United States total population that make up the tech sector all mostly men.

Oh yeah... Heads up Git can only store developer like files. It's not great at storing binaries and word documentations for version control. It's meant to be used for development and system configuration purposes only.

__BONUS__ Use `echo` to see what's behind `$HOME`.
