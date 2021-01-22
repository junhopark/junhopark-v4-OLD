---
title: Writing and deploying a simple application using Java 8 + Spark
layout: posts
---

I recently discovered [Spark](http://sparkjava.com/), which advertises itself as a "micro framework for creating web applications in Java 8 with minimal effort".  Like many developers, I'm a sucker for using the simplest tools possible to build and deliver applications so I gave Spark a try.  I wanted something that runs not only on my laptop but an application that I can easily deploy.

## Relevant technologies
Here's the list of relevant technologies I'm using to build and deploy my application I'm calling "Hellooo World":

* OS X - El Capitan
* Heroku
* IntelliJ IDEA Ultimate 16.2
* Java 8 (JDK 1.8.0_45)
* Spark Framework 2.5

## The steps

Create an account on [Heroku](https://www.heroku.com/) if you don't already have an account.  Log in on Heroku.

Create a new application in Heroku.  For the purposes of this blog post, I'm naming my new application: **hellooo-world**

In IntelliJ IDEA, go to: *File* > *New* > *Project*.  Select *Gradle* from the left-hand side.  Underneath *Additional Libraries and Frameworks*, leave *Java* checked.  Everything else should be left un-checked.  Click *Next*.
![](/assets/img/java-spark/pic_1.png)

Set *GroupId* and *ArtifactId* to the application name you assigned above (ie, **hellooo-world**).  Leave *Version* at *1.0-SNAPSHOT*.  Click *Next*.
![](/assets/img/java-spark/pic_7.png)

Select the *Use auto-import* checkbox.  Set *Gradle JVM* to *1.8*.  Click *Next*.
![](/assets/img/java-spark/pic_2.png)

Set *Project location* to where you would like your project to live in and click *Finish*.  FYI, I'm setting mine to the following: **~/workspace/java\_spark\_projects/hellooo-world**
![](/assets/img/java-spark/pic_8.png)

Open up a Terminal window on your computer and log into Heroku:

    jpark$ heroku login

In Terminal, go to the project directory and set the directory as a Git repository.  And then go ahead and add the newly created created Heroku application as a remote Git repository:

    jpark$ cd ~/workspace/java_spark_projects/hellooo-world
    jpark$ git init
    jpark$ heroku git:remote -a hellooo-world

Go back to IntelliJ IDEA.  Open up *build.gradle*.  This is what the file should look like for you right now (Depending on the version of IntelliJ IDEA you're using it may not be exact but should be pretty close to it):

    group 'hellooo-world'
    version '1.0-SNAPSHOT'

    apply plugin: 'java'

    sourceCompatibility = 1.5

    repositories {
        mavenCentral()
    }

    dependencies {
        testCompile group: 'junit', name: 'junit', version: '4.11'
    }

We're going to need to update *build.gradle* so that we can utilize Spark and enable the application to run both locally as well as on Heroku.  Update the file as follows:

    group 'hellooo-world'
    version '1.0-SNAPSHOT'

    apply plugin: 'java'

    // We want to use Java 8
    sourceCompatibility = 1.8

    repositories {
        mavenCentral()
    }

    dependencies {
        compile 'com.sparkjava:spark-core:2.5' // Spark 2.5 is the version we would like to use
        compile 'org.slf4j:slf4j-simple:1.7.21' // Without this, you will get SLF4J-related error with more recent versions of Spark
        testCompile group: 'junit', name: 'junit', version: '4.+'
    }

    // This task is needed by Heroku
    task stage {
        dependsOn build
    }

    // This task copies dependencies that are pulled down from Maven
    // and copies into a directory specified in Procfile
    task copyToLib(type: Copy) {
        into "$buildDir/libs"
        from(configurations.compile)
    }
    stage.dependsOn(copyToLib)

Let's create a Java main method that will make your application run.  First, you'll want to create the following folder structure at the project root: **/src/main/java**

Inside of the */src/main/java* directory, let's create a new Java package.  We'll call it the following: **com.hellooo**.  Inside of this package, let's create **Main.java**.  This is what my directory structure now looks like: **~/workspace/java\_spark\_projects/hellooo-world/src/main/java/com/hellooo/Main.java**

In *Main.java*, let's create our main method.  Your code should look as follows:

    package com.hellooo;

    import spark.Spark;

    import static spark.Spark.get;

    public class Main {
      public static void main(String[] args) {

        // In order for this to work on Heroku, we need to allow Heroku to set the port number
        final String portNumber = System.getenv("PORT");
        if (portNumber != null) {
          Spark.port(Integer.parseInt(portNumber));
        }

        get("/hello", (req, res) -> "Hellooo, World!");
      }
    }

It's very important that we allow Heroku to set the port number that this application will run on.  Without allowing Heroku to set the port number, your application will NOT run on Heroku (trust me - It took me a long time to figure this out).

We need to create a file and call it **Procfile**.  This is a file that Heroku needs to understand how to run your application.  Create this file at the root of your project directory.  It should contain the following single line:

    web: java $JAVA_OPTS -cp build/classes:build/libs/* com.hellooo.Main

Let's see if your application runs locally.  Open up *Main.java* > Right-click anywhere inside of this class > Select *Debug 'Main.main'*.

Once the Spark server has started (should only take a few seconds), open up a browser window and go to the following URL to see a *Hellooo, World!* message: **http://localhost:4567/hello**

We're now almost ready to push the changes up to Heroku.  But before you do, we've got a few things to take care of.  First - let's tell Git you're not going to include certain files and directories when committing (and pushing up) your code changes.  Create a file called **.gitignore** at the root of your project and add the following lines:

    .idea
    .gradle
    build

Let's go ahead and commit your changes.  Go to the project root in Terminal.  And then execute the following lines:

    jpark$ git add .
    jpark$ git commit -m "Initial working version of Hellooo World"
    jpark$ git push heroku master

Open up your browser and go to the project URL on Heroku followed by **/hello**.  For me, it's the following URL: **https://hellooo-world.herokuapp.com/hello**

You should now see a *Hellooo, World!* message.  If you're not sure what the URL of your Heroku project is, go to your project root in Terminal and execute the *heroku domains* command, like this:

    jpark$ heroku domains
    === hellooo-world Heroku Domain
    hellooo-world.herokuapp.com

That's it!  You can go to the [project repo on Github](https://github.com/junhopark/hellooo-world) to look at the code.
