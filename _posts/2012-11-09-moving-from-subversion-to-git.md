---
layout: posts
---

Last Thursday, my team made a successful transition from Subversion to Git.  Here are some thoughts after having been on Git as a team for about a week now:

### Things I like
* **Local commits:** I love that code can be committed locally.  And that I can commit much more frequently.  It helps me to work in a much more iterative fashion.
* **Easy branching & merging:** I love that branching & merging is a super lightweight task in Git (unlike Subversion).  Local branching makes it much easier for me to work on multiple different things concurrently in the same codebase.

### Things I don't like
* **Git integration in IntelliJ IDEA:** Obviously this isn't Git's fault, but something still worth mentioning.  Since Subversion integration in IntelliJ is simply flawless in my opinion, I (incorrectly) assumed that Git integration in IntelliJ would be just as amazing (We're on IntelliJ IDEA 11, BTW).  Well, I've found that there's definitely some room for improvement w/ Git integration in IntelliJ and the worst part is that you cannot rely solely on IntelliJ to meet all of your Git needs.  When I was on Subversion, I almost never had to execute Subversion commands outside of IntelliJ.  With Git, I pretty much have to work inside of both IntelliJ AND Git Bash, which slows me down since now I have to deal with 2 different applications to get work done.
* **Added complexity:**  Compared to Subversion, Git is more powerful but it is also more complex.  I'm sure I'll eventually come to a point where I find Git easy, but I'm definitely not there right now and neither are any of the folks on my team.

### Miscellaneous thoughts
* **Revision IDs:** Prior to moving over to Git, I thought that I was going to miss Subversion's sequential revision numbers since Git uses SHA-1 hashes as its unique revision IDs.  I know it's only been a week but this is something I haven't missed at all.
* **git status:** I've learned this past week that *git status* is about the most helpful command in Git.  Frequently executing *git status* in Git Bash has helped me smooth out my troubles w/ Git.
