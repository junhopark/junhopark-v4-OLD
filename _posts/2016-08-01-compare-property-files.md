---
layout: posts
---

I've been working on a rather massive refactoring work that involves changing how Java properties files are organized.  It's vitally important that the properties files from pre-refactoring work matches up 100% with the post-refactoring work and I was surprised to see that there isn't a simple tool out there that allows me compare between 2 Java properties files (or, perhaps the tool is out there but I just couldn't find it).  I was in need of something a tad bit more sophisticated than simply doing text comparisons.  For instance, if I have the following 2 properties files:

    [PROPERTIES FILE A]
    name=bobby
    age=55

    [PROPERTIES FILE B]
    age = 55
    name = bobby

I wanted my tool to tell me that those 2 properties files are exactly the same.  I figured this was a good opportunity for me to create a simple online tool that serves this purpose so I went to work.  I wanted to achieve something very similar to what the [Text Compare](https://text-compare.com/) tool has achieved.

I decided to build my application using the [Jetty server](http://www.eclipse.org/jetty/) and host it on [Heroku](https://www.heroku.com/).  I decided to go with these 2 tools because I've built a number of small applications that utilize these 2 technologies and they make it extremely easy for me to get an application up and running in a hurry.  I decided to add my project on my existing [CloudFlare](https://www.cloudflare.com) account to take advantage of its CDN and WAF.  I decided to use [Boostrap](http://getbootstrap.com/) for as my CSS framework so that I can get something that looks semi-presentable up and running without too much trouble .  I created the favicon using [X-Icon Editor](http://www.xiconeditor.com/).  My IDE of choice for this project was [IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/)--my go-to IDE.  I decided to push up my finished work to [GitHub](https://github.com/junhopark/compare-property-files).  As you will see, there isn't very much code.  The entire project consists of 2 JSPs (1 for the primary page and another for a generic semi-user friendly error page), a servlet that handles the incoming POST logic from the JSP, and a utility class that handles the comparison logic.

Here's the link to the finished product: [https://comparepropertyfiles.com](https://comparepropertyfiles.com/)
