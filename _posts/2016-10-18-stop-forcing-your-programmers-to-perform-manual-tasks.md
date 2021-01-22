---
layout: posts
---

Stop forcing your programmers to perform mindless manual tasks that could be handled via programmatic means.  And if you're a programmer who is in the unfortunate position of having to perform mind-numbing manual tasks on a regular basis, you need to find a way to replace such tasks by writing a script, building a feature, leveraging a third party tool, etc.

By the way, when I say "programmer" I mean someone with some sort of programming/scripting/technical skills, including but not limited to developers, QA folks, DBAs, and system administrators.

Most places I've worked at have a set of mindless manual tasks that certain individuals (tends to be those with privileged system and/or database access) have to perform on a regular basis.  Here are the usual cited reasons for the existence of such tasks:

* It takes someone X minutes to do it every Y days/weeks/months.  It would take Z hours/days/weeks to automate it and the cost to do this sort of work is just not justifiable from an ROI standpoint.
* We've always done it that way.  Let's not change something that's been working for a long time.
* It's a pretty simple task, right?  And you've gotten really good at it.  Sorry - we all have aspects of our jobs we don't particularly enjoy doing.


I'm not going to make an argument that every single mindless manual task needs to be retired.  Sure, if the manual task needs to be performed once every few months & it only takes someone 5 - 10 minutes to get the job done AND the manual task is complicated enough that it would take someone 5 weeks to automate it, then perhaps it's best to leave it alone.  From my experience, however, automating most manual tasks are not that difficult.  It's easy to forget to take some of the following items into account when thinking about the potential benefits of replacing a manual process with an automated one:

### Less error-prone
Sure, it's dead easy & quick to write a SQL statement that updates a single record in the users table.  But do you know how easy it is to forget to include the WHERE clause at the end and thereby update every single record in your production users table and set everyone's first name to foobar?  I've come dangerously close to doing something like this on a few occasions.  I'm sure there are people out there who've lost jobs this way.  And the unfortunate thing is that it could've been prevented.


### Minimize interruptions
Sure, it only takes 5 minutes to manually run that script on that server every X days or weeks.  It's very common, though, for these sorts of manual tasks to be time sensitive and as such, you're now regularly forcing your programmer to be regularly interrupted from his valuable heads down time.

### Enables the "customer" get what she wants faster
Computers are usually (always?) faster than humans when it comes to handling these sorts of manual tasks.  When a "customer" (could be an employee, a client, etc.) has to wait to get what she wants because a certain manual task needs to be performed first, that can be a rather frustrating experience.  Always strive to enable your employees/clients/users/etc. to get what they want as quickly as possible the way that they want it.

### No need for knowledge transfer
Even if the manual task that a certain someone on your team has been performing is mindlessly simple, there is probably a need for knowledge transfer of some sort to take place if that individual were to leave your team.  Well, there's not going to be a need for knowledge transfer to take place if the manual task doesn't even exist in the first place.

### No documentation to maintain
Maybe you're not worried about transferring knowledge because you have all of your manual tasks documented.  Well, documentations tend to go out of date.  I've yet to work with someone who is able to keep all of his documentation up to date at all times.

### Increased job satisfaction & commitment
Let's say that you have an employee on your team who is used to performing a particular mindless task on a regular basis.  If you were to walk up to this individual and ask her "Hey, I noticed you do this XYZ thing every 2 weeks.  Do you think you can come up with a way to handle it in an automated fashion?" - chances are very good that this would be beautiful music to her ears (provided that she has the necessary skill set to get the job done).  This is an opportunity that this employee of yours can now use to exercise her technical skills, engineering creativity, and can lead to an increased sense of ownership over her role on your team.

When I started working at Cappex.com there were way too many of these sorts of mindless manual tasks that some folks on the team were regularly have to perform.  While there are still some of these tasks around (certainly more than I would like), we've made solid progress, especially in the past year, in retiring these manual tasks.  I'm hopeful that sometime within the next year there will be ZERO such mindless tasks that my team members have to perform on a regular basis.
