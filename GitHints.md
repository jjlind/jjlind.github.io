
HINTS at solutions to various problems based on experience.

Problem #1:
--------

    Files on remote repository is OK, but the local files have been fucked up.

Solution #1:
-----------

    One way to get out of it is to delete all your files including the '.git' (you may want
    to copy all to a backup directory first though).

    Then in a blank project directory do

        | => git init
        Initialized empty Git repository in /Users/johnny/repos/jjlind.github.io/.git/

        | => git pull
        There is no tracking information for the current branch.
        Please specify which branch you want to merge with.

    That obviously didn't work.

         => git remote add origin https://github.com/jjlind/jjlind.github.io

    Now the connection to remote should be established,

        | => git pull
        remote: Enumerating objects: 79, done.
        remote: Counting objects: 100% (79/79), done.
        remote: Compressing objects: 100% (52/52), done.
        remote: Total 79 (delta 24), reused 72 (delta 20), pack-reused 0
        Unpacking objects: 100% (79/79), done.
        From https://github.com/jjlind/jjlind.github.io
         * [new branch]      master     -> origin/master
        There is no tracking information for the current branch.
        Please specify which branch you want to merge with.

    and git now seems to have pulled something, but

        | => ll
        total 0
        drwxrwxr-x  11 johnny  staff   374B May  8 20:28 .git/

    directory is still empty (apart from .git/). Let's try again with 'master' specification.

        | => git pull master
        fatal: 'master' does not appear to be a git repository
        fatal: Could not read from remote repository.

        Please make sure you have the correct access rights
        and the repository exists.

    That seems to fail, so lets try another thing.

        | => git checkout master
        Branch 'master' set up to track remote branch 'master' from 'origin'.
        Already on 'master'

        | => ll
        total 16
        -rw-rw-r--   1 johnny  staff   6.0K May  8 20:30 .DS_Store
        drwxrwxr-x  12 johnny  staff   408B May  8 20:30 .git/
        -rw-rw-r--   1 johnny  staff   101B May  8 20:30 README.md
        drwxrwxr-x   6 johnny  staff   204B May  8 20:30 _includes/
        drwxrwxr-x   3 johnny  staff   102B May  8 20:30 _layouts/
        drwxrwxr-x   6 johnny  staff   204B May  8 20:30 _site/
        drwxrwxr-x   4 johnny  staff   136B May  8 20:30 css/
        drwxrwxr-x   3 johnny  staff   102B May  8 20:30 images/
        -rw-rw-r--   1 johnny  staff    24B May  8 20:30 index.html

    Yeah. We got the files on local working directory now, and the git log shows how far we've come.

        | => git log
        commit 1a55b0e4690497e4d156051d0f9aff7b0fe1ae16 (HEAD -> master, origin/master)
        Author: Johnny <git@lindeskovhus.dk>
        Date:   Thu May 2 19:49:29 2019 +0200

            Add new files from chapter 5

        commit 2d6c60a47cb5b53cbd6fcf58f6d4adcfb1334487
        Author: Johnny <git@lindeskovhus.dk>
        Date:   Thu May 2 19:47:26 2019 +0200

            Complete Chapter 5

        commit bbabb71119b1366e36cb4e1beb437dcadf67ee08
        Author: Johnny <git@lindeskovhus.dk>
        Date:   Tue Apr 30 14:20:43 2019 +0200

            Complete Chapter 5.7, but skip the final Exercises 5.7.6

        etc.
        etc.
        etc.

    And during the whole "solution" above, "jekyll" server kept tracking the files, so that they
    could be served - if present.

--------------------------------------------------------------------------------------------------------

Create a new branch for experiments.
====================================

    git checkout -b excercises-6-2-1        <-- Creates a new branch for excercises.

    git checkout master                     <-- Switches back to main branch; the trunk.

    git branch -d excercises-6-2-1          <-- Remove the branch and forget about the changes.
