---
layout: posts
---

Yesterday at work I had a need to copy a single from an existing Git repository to a newly created Git repository while maintaining all of the commit history associated with this file.  I did some Googling around and the most straight forward solution I came across was described on the following page: [http://blog.neutrino.es/2012/git-copy-a-file-or-directory-from-another-repository-preserving-history/](http://blog.neutrino.es/2012/git-copy-a-file-or-directory-from-another-repository-preserving-history/) (thank you!)

I wanted to simplify the steps even further and add a bit more explanation.  Here goes.

1) Let's say that you want to copy ***hello.txt*** from a repo called ***existing-repo*** *(Located at: ~/existing-repo)* to ***new-repo*** *(Located at: ~/new-repo)*.

2) Create a temporary directory (let's call it ***temporary-patches***) where all of temporary Git patch files that are created as a result of this process will be located.

    cd ~/

    mkdir temporary-patches

3) Change directory to ***existing-repo*** and generate patch files that contain the commit history of the file that you would like to move:

    cd ~/existing-repo

    git format-patch -o ~/temporary-patches $(git log ~/existing-repo/hello.txt|grep ^commit|tail -1|awk '{print $2}') ~/existing-repo/hello.txt

Note that if the file you're wanting to copy is a file that was made as a part of the initial commit of the existing repository - you'll run into like the following:

    fatal: ambiguous argument '140f6efe94bfe9552474097cd0c658c94a292f46^..HEAD': unknown revision or path not in the working tree.

See one of the comments on [http://blog.neutrino.es/2012/git-copy-a-file-or-directory-from-another-repository-preserving-history/](http://blog.neutrino.es/2012/git-copy-a-file-or-directory-from-another-repository-preserving-history/) that describes how to handle this situation (Do a text search for *"This does not work if the file was made in the initial commit"*).

4) Change directory to ***new-repo*** and then apply the patch files that were generated as a result of the above command:

    cd ~/new-repo

    git am ~/temporary-patches/*.patch

If you run into an error here, chances are good that you've got 1 or more uncommitted changes in your current branch.  An error I came across was the following:

    fatal: previous rebase directory .git/rebase-apply still exists but mbox given.

5) Confirm that the commit history has been preserved after the file was moved.

    git log hello.txt

6) When you do a git status you'll see that there is nothing for you to commit.  All done!

*******EDIT on 9/25/2016*******

I recently had to do this (copying files from one Git repo to another Git repo while maintaining history) again and ran across the issue I noted in step #3 above.  Here's what I ended up doing:

    cd ~/existing-repo

    git format-patch -o ~/temporary-patches --root [Git commit hash of the very first commit] ~/existing-repo/hello.txt

    git format-patch -o ~/temporary-patches $(git log ~/existing-repo/hello.txt|grep ^commit|tail -1|awk '{print $2}') ~/existing-repo/hello.txt

    cd ~/temporary-patches

    mv 0001-Very-first-commit.patch 0000-Very-first-commit.patch
