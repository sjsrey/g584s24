## jumping around

    cd
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ cd
    jupyter-serge584s23@geo-rey-srv2:~$ git clone https://github.com/rupa/z.git
    Cloning into 'z'...
    remote: Enumerating objects: 800, done.
    remote: Counting objects: 100% (18/18), done.
    remote: Compressing objects: 100% (12/12), done.
    remote: Total 800 (delta 8), reused 15 (delta 6), pack-reused 782
    Receiving objects: 100% (800/800), 161.14 KiB | 1.73 MiB/s, done.
    Resolving deltas: 100% (363/363), done.

    cp .bashrc .bashrc.bak
    nano .bashrc

    # add the line
    . ~/z/z.sh

    tail -1 .bashrc

    jupyter-serge584s23@geo-rey-srv2:~$ tail -1 .bashrc
    . ~/z/z.sh

    source ~/.bashrc

Now cd around a bunch

Type `z` to get a listing of recently visited directories

To jump to one, type `z pattern` where `pattern` should be a substring
of the directory you want to jump to.

No more having to manually type long paths to get to where you want to
go.

Note, this works even after logging out or closing the terminal.

The data is stored in the file `~/.z` if you are interested.

## create a remote on github

\![\[Pasted image 20230220171356.png\]\]

\![\[Pasted image 20230220170657.png\]\]

\![\[Pasted image 20230220171442.png\]\]

we will come back to this in a moment. for now lets make sure we are in
are local repository directory:

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ pwd

    /home/jupyter-serge584s23/work/git/planets

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ ls -al

    total 28
    drwxr-xr-x 4 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 16 12:44 .
    drwxr-xr-x 3 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 16 11:20 ..
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23    0 Feb 16 12:10 a.dat
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23    0 Feb 16 12:10 b.dat
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23    0 Feb 16 12:10 c.dat
    drwxr-xr-x 8 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 16 12:44 .git
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23   15 Feb 16 12:14 .gitignore
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23   91 Feb 16 12:02 mars.txt
    -rw-r--r-- 1 jupyter-serge584s23 jupyter-serge584s23   49 Feb 16 12:44 moon.txt
    drwxr-xr-x 2 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 16 12:10 results

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git status

    On branch main
    nothing to commit, working tree clean

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git remote -v
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ 

## ssh keys

    jupyter-serge584s23@geo-rey-srv2:~$ ssh-keygen -t rsa
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/jupyter-serge584s23/.ssh/id_rsa): 
    Created directory '/home/jupyter-serge584s23/.ssh'.
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/jupyter-serge584s23/.ssh/id_rsa
    Your public key has been saved in /home/jupyter-serge584s23/.ssh/id_rsa.pub
    The key fingerprint is:
    SHA256:xRueWRVTnHYxfri6WuEpzXZJHW7E252NikYNpzIB+5o jupyter-serge584s23@geo-rey-srv2
    The key's randomart image is:
    +---[RSA 3072]----+
    |      .       +*+|
    |       o .   .o=+|
    |      . . = o o=o|
    |       . + @  o+O|
    |        S B o +==|
    |       o + = *.. |
    |      E   + X o  |
    |         . + o   |
    |          ...    |
    +----[SHA256]-----+
    jupyter-serge584s23@geo-rey-srv2:~$ 

    ls .ssh

    id_rsa  id_rsa.pub

    upyter-serge584s23@geo-rey-srv2:~$ ls -al ~/.ssh

    total 16
    drwx------  2 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 20 16:47 .
    drwxr-x--- 11 jupyter-serge584s23 jupyter-serge584s23 4096 Feb 20 16:47 ..
    -rw-------  1 jupyter-serge584s23 jupyter-serge584s23 2675 Feb 20 16:47 id_rsa
    -rw-r--r--  1 jupyter-serge584s23 jupyter-serge584s23  586 Feb 20 16:47 id_rsa.pub

Check if we can authenticate

    jupyter-serge584s23@geo-rey-srv2:~$ ssh -T git@github.com
    The authenticity of host 'github.com (192.30.255.113)' can't be established.
    ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
    This key is not known by any other names
    Are you sure you want to continue connecting (yes/no/[fingerprint])? y
    Please type 'yes', 'no' or the fingerprint: yes
    Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
    git@github.com: Permission denied (publickey).

Right, we need to first add our public key on github

    cat ~/.ssh/id_rsa.pub

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCv4y7kR22zjaNYPIP8L/q/lcfWPtltLOZ86vszqpwqEaMFDWaQ366sGEc0hYRjZMbFKxNSy9d7PJnOq0ozCgoNn69dNmXx+M71TM2E7vlUjCZCo9owEfIuDf6o519uRE4Qf2aKQC1g3M+imZn9gnZtI39cQsKPM1h0Wg417ZgdgyC3k4bep7puxiko3R3gEaXVUEPHtodEfI7hwUsV62J3CWBIx5yQzwAGJz7VtYQIB94/5jNUnIGtRQyHFcplxKJ/weM6LkQt5Uxql9oliVHYqp8KBu63PPxXt8qusKGJrnmkccHd6ox8i3LIp2XRImdm8DittHuMJRgJiLa/HQtr9jyHoIx8voztvvbyRCOCzRwWKe9hZXWw/Xp+xbKsoH826e4Iqgp56LzmVB7NKEYf1jArrLEqO+DQWEJkXl8IidqUGNvJ8I4tFRZrRm6URNClseZ31gSsVMAO/HHwoVlVw7s32tmEQ8c+ISGL+llRU/rI5yKPSBLb28YDckes7jc= jupyter-serge584s23@geo-rey-srv2

\![\[Pasted image 20230220165448.png\]\]

\![\[Pasted image 20230220165614.png\]\]

\![\[Pasted image 20230220165800.png\]\]

\![\[Pasted image 20230220165837.png\]\]

\![\[Pasted image 20230220170035.png\]\]

\![\[Pasted image 20230220170132.png\]\]

Now try authenticating again, which will prompt you for your passphrase

    jupyter-serge584s23@geo-rey-srv2:~$ ssh -T git@github.com
    Enter passphrase for key '/home/jupyter-serge584s23/.ssh/id_rsa': 

    Hi sjsrey! You've successfully authenticated, but GitHub does not provide shell access.
    jupyter-serge584s23@geo-rey-srv2:~$ 

Now we add a new remote (remember your passphrase as they will ask for
it)

    git remote add origin git@github.com:sjsrey/planets.git
    git branch -M main
    git push -u origin main
    Enter passphrase for key '/home/jupyter-serge584s23/.ssh/id_rsa': 

    Enumerating objects: 15, done.
    Counting objects: 100% (15/15), done.
    Delta compression using up to 32 threads
    Compressing objects: 100% (10/10), done.
    Writing objects: 100% (15/15), 1.29 KiB | 1.29 MiB/s, done.
    Total 15 (delta 3), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (3/3), done.
    To github.com:sjsrey/planets.git
     * [new branch]      main -> main
    Branch 'main' set up to track remote branch 'main' from 'origin'.
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ 

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git remote -v

    origin  git@github.com:sjsrey/planets.git (fetch)
    origin  git@github.com:sjsrey/planets.git (push)

\![\[Pasted image 20230220171920.png\]\]

\![\[Pasted image 20230220172005.png\]\]

## Adding a ssh-agent

    jupyter-serge584s23@geo-rey-srv2:~$ eval "$(ssh-agent -s)" 
    Agent pid 327199
    jupyter-serge584s23@geo-rey-srv2:~$ ssh-add ~/.ssh/id_rsa 
    Enter passphrase for /home/jupyter-serge584s23/.ssh/id_rsa: 
    Identity added: /home/jupyter-serge584s23/.ssh/id_rsa (jupyter-serge584s23@geo-rey-srv2)

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ nano README.md
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ ls
    a.dat  b.dat  c.dat  mars.txt  moon.txt  README.md  results
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            README.md

    nothing added to commit but untracked files present (use "git add" to track)
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git add README.md 
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git commit -m 'Add a README'
    [main 864e428] Add a README
     1 file changed, 3 insertions(+)
     create mode 100644 README.md
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git push origin main
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 32 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 375 bytes | 375.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To github.com:sjsrey/planets.git
       68a5f4f..864e428  main -> main
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ 

\![\[Pasted image 20230220173424.png\]\]

## Setting up ssh-agent

Make a backup of `~/.bashrc`

    cd
    cp .bashrc .bashrc.bak
    nano .bashrc

At the bottom of the file add the following
([Source](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases?platform=windows)):


    env=~/.ssh/agent.env

    agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

    agent_start () {
        (umask 077; ssh-agent >| "$env")
        . "$env" >| /dev/null ; }

    agent_load_env

    # agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
    agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

    if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
        agent_start
        ssh-add
    elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
        ssh-add
    fi

    unset env

Write and exit the file. Close the terminal tab.

Launch a new terminal and you should be prompted for your password.

\![\[Pasted image 20230220174112.png\]\]

\![\[Pasted image 20230220174144.png\]\]

\![\[Pasted image 20230220174224.png\]\]

From here forward you no longer will be prompted for password when
pushing to github. (as long as that terminal stays around)

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ nano README.md 
    cat README.md

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ cat README.md 
    # Planets Project


    Research on planets

    Test after ssh-agent


    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git add README.md 
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git commit -m 'Note on ssh-agent'
    [main be51b2e] Note on ssh-agent
     1 file changed, 3 insertions(+)
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git push origin main
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 32 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 320 bytes | 320.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    To github.com:sjsrey/planets.git
       864e428..be51b2e  main -> main
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ 

## Pulling from remotes

    git status
    On branch main
    Your branch is up to date with 'origin/main'.

    nothing to commit, working tree clean

Create changes on github to the README.md file

make sure to commit the changes there

    git status
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    nothing to commit, working tree clean

Fetch will pull any remote changes

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git fetch
    remote: Enumerating objects: 5, done.
    remote: Counting objects: 100% (5/5), done.
    remote: Compressing objects: 100% (3/3), done.
    Unpacking objects: 100% (3/3), 707 bytes | 707.00 KiB/s, done.
    remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
    From github.com:sjsrey/planets
       be51b2e..a0279db  main       -> origin/main


    git status
    On branch main
    Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
      (use "git pull" to update your local branch)

    nothing to commit, working tree clean

This tells us there are changes on the remote that we don't have
locally. To get them, we follow the helpful suggestions:

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git pull
    Updating be51b2e..a0279db
    Fast-forward
     README.md | 3 +++
     1 file changed, 3 insertions(+)

    git status
    On branch main
    Your branch is up to date with 'origin/main'.

    nothing to commit, working tree clean

So good practice is everytime you sit down to do some work on a local
repository:

1.  git fetch \# to see if there have been changes on the remote
2.  git pull \# if there have been
3.  do you work locally and then push to origin when done

## Conflicts

Now that both repositories, local and remote, are identical, we are
going to create a *conflict*.

These can arise when working on collaborative projects where multiple
people are changing the same files, or on your individual work, where
you may be working from different locations and forgot that the past you
had changed a file on a remote while current you is happily working on
the same part of the file on a local repository.

To do this, let's go all Ohio State and on github edit the readme so the
title is "The Planets Project".

Now on the local repository, edit the same line, but let's call it "My
Planet Project" Locally:

    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    jupyter-serge584s23@geo-rey-srv2:~/work/git/planets$ 

git pull (to show conflict)

### How to resolve a conflict

explain markers

edit file to reconcile conflict

git add git commit

git push

note conflicts only involve changes to the same line

# collaboration

see moleskein for the git flow diagram all team members should have
forked the shared repository (except for the person who created it)

fork if you have not

https://github.com/raffaelen/Identifying-Regional-Employment-Centers
https://github.com/elizabeth-bushnell/15_minute_city_584project
https://github.com/rbilchak/Balboa_Park_Mapping
https://github.com/hannahsamy/sd_agriculture_project
https://github.com/fiendskrah/584-education-inequality

clone the group project into your jupyter hub account

make a directory for the 584project cd into 584project clone your fork

add the upstream remote

walk them through this for the course project

1.  fork
2.  clone
3.  add upstream
4.  pull from upstream
5.  branch on local
6.  make changes to README.md
7.  add, commit
8.  push branch to origin
9.  PR into upstream from origin
