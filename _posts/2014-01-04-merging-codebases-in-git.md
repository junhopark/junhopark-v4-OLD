---
layout: posts
---

A couple of weeks ago, I had to merge one codebase into another codebase and after a lot of searching for solutions on the web, I came across a solution that has worked well for my team.  By following these steps, we were able to merge the two codebases and were able to retain the commit history of both codebases (without having to execute ***git log --follow***).

Listed below are the steps that were followed.  Note that I'll be referring to the following 2 codebases:  *codebase-A* and *codebase-B*.  codebase-B is the codebase that will be *merged into* codebase-A.

1. Clone codebase-b into another directory.  Change directory to the parent directory of codebase-b (***cd ~/development***) and then execute: ***git clone --no-hardlinks ~/development/codebase-b codebase-b***

2. Change to the newly created directory: ***cd ~/development/codebase-b***

3. And then execute: ***git remote rm origin***

4. While in the codebase-b directory, move all of the files inside it (except for the .git folder) into a newly created sub-directory (ie, codebase-b-files).  ie, if you have 2 files inside of ~/development/codebase-b, the 2 files should now be inside of ~/development/codebase-b/codebase-b-files.  When moving files, use the ***git mv*** command.  You'll see the benefits of moving files around when it comes time to merging codebase-b into codebase-a.

5. Go ahead and do a Git commit of all of your changes inside of the codebase-b directory.

6. Change directory to codebase-a: ***cd ~/development/codebase-a***

7. Execute the following: ***git remote add codebase-b ~/development/codebase-b***

8. And then execute: ***git pull codebase-b***

9. Now that you've pulled in codebase-b, you can go ahead and remove the association to codebase-b: ***git remote rm codebase-b***

10. At this point, you should see codebase-b merged into codebase-a.

11. From this point on, all you have left to do is to move the merged files around in codebase-a.  Use the ***git mv*** command when moving files so as to preserve the commit history.

Credits: [Merge Two Git Repositories Into One](http://jasonkarns.com/blog/merge-two-git-repositories-into-one/)
