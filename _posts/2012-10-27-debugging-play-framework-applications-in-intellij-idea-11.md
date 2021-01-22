---
layout: posts
---

I just spent 30 minutes on Google trying to figure out how to debug my Play application in IntelliJ when it should've taken me 1 minute, tops.

Follow these simple steps to debug your Play framework application in IntelliJ IDEA 11:

0) If you haven't yet converted your application to a IntelliJ project, open up a console/terminal > go to the application root > and run ***play idea***.

1) While you're still at the project root, run ***play debug***.

2) Wait a few seconds for Play to finish whatever it's doing then run ***run***.

3) In IntelliJ, click Run > Edit Configurations > '+' icon > Remote.  Enter the following information then click Ok.

Name: Play! (or whatever you'd like it to be)
Transport: Socket  
Debugger mode: Attach
Host: localhost  
Port: 9999  
Set the module drop-down list to your application module.  

![IntelliJ](/assets/img/debug-play-in-intellij.png)

4) Go to Run > Debug > Select 'Play!'.

The end.
