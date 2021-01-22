---
layout: posts
---

After years and years of writing software for the web, I decided that it's about time I start tinkering around with mobile apps.  I decided to use the following tools to build my very first Android app:

* **PhoneGap...** since I've heard PhoneGap mentioned numerous times by various developers & was drawn to its write-once-run-it-everywhere principle.  I love that I can build mobile apps using HTML + CSS + JavaScript.
* **jQuery Mobile...**: since I use jQuery pretty much on a daily basis at work. (Note: This was my first time using jQuery Mobile)
* **IntelliJ IDEA...**: It's the best IDE there is.

I wanted to build something *super* simple for my very first app.  After thinking about it for a bit, I decided that I would build a random number generator.  Super simple.  Nothing more than 2 text fields (Min & Max values), a button, and some simple logic to generate and render the number.

If you're curious, here's how I did it, step by step (on MacBook Air):

**Opened a new terminal and created a new PhoneGap project.**

    > cd ~/workspace/phonegap_projects
    > ~/workspace/phonegap-2.9.0/lib/android/bin/create random_number_generator

**Opened IntelliJ IDEA and created a new project by going to:** New Project > Create project from existing sources > **and set the project file location to:** ~/workspace/phonegap_projects/random_number_generator

**I went to [jQuery Mobile Theme Roller](http://jquerymobile.com/themeroller/ "jQuery Mobile Theme Roller") and created a new custom theme.  I then downloaded the zip file and unzipped it inside of the following directory in my PhoneGap project:** /assets/www/

**Made the following changes to** index.html

    ...
    <link rel="stylesheet" href="themes/custom-blue-pink.css"/>
    <link rel="stylesheet" href="css/jquery.mobile.structure-1.3.1.min.css"/>
    <link rel="stylesheet" href="css/mystyle.css"/>
    ...
    <script type="text/javascript" src="js/jquery-2.0.3.min.js"></script>
    <script type="text/javascript" src="js/jquery.mobile-1.3.1.min.js"></script>
    ...

**Made some further edits to** index.html **and added in the following** (I had to reference the jQuery Mobile site on this)

    ...
    <div data-role="page" data-theme="a">
      <div data-role="header" data-position="inline">
        <h1>Random # Generator</h1>
      </div>
      <div data-role="content" data-theme="a">
        <label for="min">Min</label>
        <input type="number" name="min" id="min" value="0" min="0" max="1000" data-theme="a"/>

        <label for="max">Max</label>
        <input type="number" name="max" id="max" value="10" min="1" max="1000" data-theme="a"/>

        <a href="#" data-role="button" data-icon="check" id="generate">Generate!</a>

        <div id="numberContainer">
          <label>Your random number is:</label>

          <h1 id="number">?</h1>
        </div>
      </div>
    </div>
    ...

**Created** /assets/www/css/mystyle.css **which contains the following:**
    #numberContainer {
      text-align: center;
      margin-top: 10%;
    }

**Modified** index.js **and added the following:**

    ...
    isValid:function (min, max) {
        return (min || min == 0) && min >= 0 && max && max > min;
    },

    displayError:function (errorMessage) {
        alert(errorMessage);
    },

    generateRandomNUmber:function () {
        var min = parseInt($('#min').val(), 10);
        var max = parseInt($('#max').val(), 10);

        if (this.isValid(min, max)) {
            var random = Math.floor(Math.random() * (max - min + 1)) + min;
            $('#number').html(random);
        } else {
            this.displayError('Please make sure your Min & Max values are valid.');
        }
    },

    attachEvents:function () {
        $('#generate').on('click', function (event) {
            event.preventDefault();
            app.generateRandomNUmber();
        })
    }
    ...

    document.addEventListener("deviceready", function () {
        app.attachEvents();
    });

**I then zipped up my project folder** (ie ~/workspace/phonegap_projects/random_number_generator) **and uploaded the zipped file to Adobe PhoneGap Build (I had to sign up first).**

**PhoneGap Build proceeded to build my project and after about a minute of waiting, it gave me an option to download my app as an .APK file.**

**I saved the .APK file to my phone (Samsung Galaxy Note) > installed Apk Installer from Google Play > and used Apk Installer to install the .APK file I downloaded from PhoneGap Build.**

And here it is:

![My first mobile app](/assets/img/random_number_generator.png)

Not too bad, especially considering that I spent mere 2 hours and that this was my very first mobile app.  And I accomplished this with 20 lines of HTML, 5 lines of CSS, and 25 lines of JavaScript.
