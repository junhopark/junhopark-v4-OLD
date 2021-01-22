---
layout: posts
---

I noticed that Heroku supports Java applications running on Jetty and since I've never worked with Jetty previously,
I thought I'd give it a go.  Please note that I'm running IntelliJ IDEA 11 on OS X Mountain Lion.

* Go to java.heroku.com
* Click on the 'Create App' button for the 'Containerless web app with Embedded Jetty'
* Clone the app Heroku created for you (ie: git clone git@heroku.com:immense-brook-1182.git)
* In IntelliJ, File > New Project > Import project from external model > Select Maven > Select the directory of your application > Click the 'Next' button a few times with default settings in place and finish the wizard.
* When the newly created project opens up in IntelliJ, open up pom.xml and add the following in the 'plugins' section:

      <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>jetty-maven-plugin</artifactId>
      </plugin>

* Click the 'Maven Projects tab' in IntelliJ > Expand the 'Plugins' section of your application > Expand 'jetty' > Right-click on 'Jetty:run' > Click on 'Run Maven Build' (OR, select the 'Debug...' option if you want to be able to debug through your application)
* Go to http://localhost:8080 in your browser.  You should see a welcome page.
* I made some changes to index.jsp > Pressed Cmd + F9 > and my changes showed up upon refreshing my browser window.
Likewise, I was able to do the same after making modifications to HelloServlet.java.

![Screenshot](/assets/img/jetty_heroku_screenshot.jpg)

Everything about this was extremely simple and straightforward *except* for having to add the jetty-maven-plugin.
That took me quite awhile to figure out but now that I have, everything seems straightforward once again.
