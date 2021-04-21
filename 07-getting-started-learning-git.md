# Getting Started Learning Git

## Basic `git` commands
- `git pull`
- `git status`
- `git branch`
- `git checkout`
- `git add`
- `git restore --staged`
- `git commit`
- `git push`

Git will save your life!

1. `git status` allows you to see the status of your current changes.
    ```
    ❯ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   03-getting-started-admin.md

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        07.5-test-your-skills.md

    no changes added to commit (use "git add" and/or "git commit -a")
    ```
2. `git branch` allows you to see the current branch you are on and other local branches you have
    ```
    ❯ git branch
    * main
    testing-stuff
    ```
    Remember that the `*` is a indicator of the branch you are currently on.
3. `git checkout` allows you to checkout a branch you want to be in. 
    ```
    ❯ git checkout testing-stuff
    M	03-getting-started-admin.md
    Switched to branch 'testing-stuff'
    ❯ git branch
    main
    * testing-stuff
    ```
4. `git add` allows you to stage files ready to be commited into the overall project locally.
    ```
    ❯ git st
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        modified:   03-getting-started-admin.md

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        07.5-test-your-skills.md
    ```
    When you have staged it you can see the file cahnged to a green color if your commandline does color.
5. If you ever need to backout the changes you thought you were going to save to the branch you want to unstage it with `git restore --staged`.
    ```
    ❯ git restore --staged 03-getting-started-admin.md
    ❯ git st
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   03-getting-started-admin.md

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        07.5-test-your-skills.md

    no changes added to commit (use "git add" and/or "git commit -a")
    ```
    This will change the `modified:   03-getting-started-admin.md` part of the output back into red. Which indicates its not going to be added into the branch.
6. Going back to when the file was staged. If you are sure you want to put them in the branch use `git commit` to add them in. Usually you want to add a message/note to the commit so use the parameter `-m "your message or note here"` with it. 

    ```
    ❯ git add 03-getting-started-admin.md
    ❯ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        modified:   03-getting-started-admin.md

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        07.5-test-your-skills.md

    ❯ git commit -m 'changes to the files'
    [main 7277853] changes to the files
    1 file changed, 181 insertions(+), 1 deletion(-)
    ```
    Once changes are commited this is only on your local branch this does not affect your branches up on the internet/project. The way for you to undo a commit is to do a hard reset. 
7. We are not going to undo the commit but actually push into the global repo up on the internet with `git push`.
    ```
    ❯ git push
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 12 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 7.42 KiB | 3.71 MiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0)
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    To https://github.com/2infinitee/learning-tech.git
    31e5acc..7277853  main -> main
    ```
8. `git pull` allows you to retrieve the latest code from the repoisitory everyone is contributing to.
    ```
    ❯ git pull
    Already up to date.
    ```
    
### Summery
There you have it the most basic git commands you should be familiar with. What are some pointers/best practices about using git? 
    - You should always run a `git pull` whenever you are going to work on a project. 
    - You should always create a branch from the latest code when you can. The rule of thumb is to do one per story. A story is kind of like a minor change and nothing too big where there are too many changes to keep track of.
    - If your workplace practices it demo your changes to a peer and show them that the code or changes work.

If you ever push code and there was a chance that someone else made changes right before you did, it will prompt you to resolve the conflecting files in `vim` or `nano` with a message that says to pull the latest change with a merge. To put it simply you can just exit out of `vim` and commit/push agian after you test the new changes pulled into your localhost. It can get complicated for merges that are trying to take affect so ask for help if you're stuck.

The other thing is once your code is up on your branch in the repo/internet/company network you want to submit a pull request (PR) to merge in your changes into the master/main branch. This will make sure that the work you've done goes into the main project code or configuration.


