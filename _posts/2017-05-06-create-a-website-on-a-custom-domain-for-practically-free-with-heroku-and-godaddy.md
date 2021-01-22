---
title: Create a Website On a Custom Domain for Practically Free With Heroku and GoDaddy
layout: posts
---

I've had several people ask me over the years what's a good & cheap way to set up a static or a dynamic website on a custom domain. One of the best things about writing a blog post is that instead of having to repeat myself I can point people to a blog post that I've written.

Anyhow, here are the steps for creating a website on a custom domain for *really* cheap with Heroku and GoDaddy. The only price you would pay is the cost of the domain name. Free hosting.

1) Register a domain name on **GoDaddy**. You don't *have to* go with GoDaddy (there are many domain registrars out there after all) but the reason why I've decided on GoDaddy at least for this blog post is because they allow you to modify DNS settings associated with their domains without having to pay extra. I've dealt with other domain registrars that don't allow for this, which is a show stopper (as far as I know) for getting your custom domain to work with an application running on Heroku.

I happened to have a spare domain - **theblameboard.com**. I'm going to use this domain for the blog post.

2) If you don't have an account on [Heroku.com](https://www.heroku.com), go ahead and create one. During the sign-up process, when you're asked for your **Primary Development Language** - I don't know that it matters what you pick here but go ahead and pick **PHP**.

![](/assets/img/heroku-godaddy/heroku_signup.png)

3) Log into Heroku and click on the **Create New App** button. Give your application a name. I know the field says it's *optional* but I'd suggest you give it some kind of a name. I'm going to call my app **blame-board**.

When I open my web browser of choice (Chrome) and go to [https://blame-board.herokuapp.com/](https://blame-board.herokuapp.com/) - I see the following:

![](/assets/img/heroku-godaddy/new_site_heroku.png)

4) Follow the steps on [this page](https://devcenter.heroku.com/articles/heroku-command-line) and install the **Heroku CLI** (Command Line Interface).

5) You're now going to need to set up a Git repository on your computer which will store all of the files for this new application.

Create a new directory for your project and initialize a Git repository:

    $ mkdir blame-board
    $ cd blame-board
    $ git init

Log into your Heroku account using the Heroku CLI and link your local Git repository to the Git repository on Heroku:

    $ heroku login
    $ heroku git:remote -a blame-board

6) For this blog post, I'm going to create a static site. The easiest way I've found to get a static site up on Heroku is to set up an application that Heroku thinks is a PHP application. To do this, create a new file **index.php**. This file should contain just the following single line:

    <?php include_once("home.html"); ?>

The sole purpose of this PHP file is to include the home.html file which you will create in the next step. Oh, that and telling Heroku that this is a PHP application. FYI - if all you have are static files (HTML, JavaScript, CSS, etc.) in your Heroku project - Heroku won't know how to deploy your application.

7) Create a new file called **home.html**. This is your "index" HTML page. I've added the following code in mine:

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>The Blame Board</title>
    </head>
    <body>
      This is The Blame Board.
    </body>
    </html>

If you want to call your "index" HTML page something other than home.html - that's totally fine. Just make sure that's reflected in the index.php file.

8) In Terminal - commit your changes to your local Git repository and push it up the repository on Heroku.

    $ git add .
    $ git commit -m "Initial commit"
    $ git push heroku master

If you see something along the lines of **"...https://blame-board.herokuapp.com/ deployed to Heroku..."** you're all set.

9) Go to [https://blame-board.herokuapp.com](https://blame-board.herokuapp.com) and verify that you can see the updates:

![](/assets/img/heroku-godaddy/index_page.png)

10) Before you can assign a custom domain to your Heroku application you need to add a credit card to your Heroku account. To do this, go to: [https://heroku.com/verify](https://heroku.com/verify)

No, Heroku won't charge you as long as you stay on the their free tier. It's a little annoying they make you add a credit card but I can't complain too much... it's still free after all.

As of this writing (May 2017) - according to [this page](https://devcenter.heroku.com/articles/free-dyno-hours) - free accounts are limited to 550 hours of server time per month. When you add a credit card to your account you're given 450 additional hours. Since there are roughly 730 hours per month the only way you can have a Heroku application running 24x7 for free is to have a credit card on your account.

11) After you've added a credit card assign a custom domain name to the Heroku application.

Go back to the Heroku dashboard in the browser. Click on the **Settings** link at the top. If you scroll down a bit, you'll see an **Add domain** button. Click that. In the modal, type in the domain name you want associated with your site staring with **www** (this is very important!). For my example I added the following: **www.theblameboard.com**

![](/assets/img/heroku-godaddy/heroku_domain.png)

If you haven't added a credit card to your Heroku account yet you will get the following error message:

**Please verify your account in order to add domains (please enter a credit card) For more information, see https://devcenter.heroku.com/categories/billing Verify now at https://heroku.com/verify**

12) Now, to finish linking your custom domain to the Heroku application you'll need to do a few things on GoDaddy. Click on the **Manage DNS** button for your domain.

Scroll down a bit and look for where it has **Type = CNAME** and **Name = www**. Click the pencil icon to the right and update **Points to** to the URL of your Heroku application WITHOUT **https://www**. I entered **blame-board.herokuapp.com** and clicked the **Save** button.

![](/assets/img/heroku-godaddy/cname_2.png)

13) If someone attempts to go to your site without the **www** subdomain (theblameboard.com), you may (probably will) want to forward the user to www (www.theblameboard.com). In the GoDaddy screen - look for the **Forwarding** section. Click the **ADD** link next to **DOMAIN**. Set it to: **http://www.theblameboard.com**

You'll probably want to leave **Forward Type** to **Permanent (301)** and **Forward only** instead of the *Forward with masking* option.

Check the **Update my nameservers and DNS settings to support this change.** checkbox.

Click **Save**.

14) In your browser, go to your domain name (eg, [www.theblameboard.com](http://www.theblameboard.com)) and verify that your Heroku application comes up. If you see a GoDaddy page instead, it mostly means that your DNS changes haven't yet propagated. From my experience, this should only take a few minutes. If you're unlucky, though, you may have to wait several hours or even several days.

15) Applications running on the free tier of Heroku will sleep if it receives no traffic in a 30 minute period ([Read this](https://devcenter.heroku.com/articles/free-dyno-hours) for more info). Once the application falls asleep, it'll take a little bit of time (10 seconds?) for it to wake up. One way to keep it from sleeping is to ping your Heroku application every so often (more frequently than 30 minutes). I use **UptimeRobot** for this. Go to [uptimerobot.com](https://uptimerobot.com/) and create an account and log in.

When you log in click on the *Add New Monitor* button. This is what my settings look like:

* Monitor Type = **HTTP(s)**
* Friendly Name = Whatever you want it to be. I'm setting mine to: **theblameboard.com**
* URL = **http://www.theblameboard.com**
* Monitoring interval: Anything less than 30 minutes.

![](/assets/img/heroku-godaddy/uptimerobot.png)

**And that's it!**

While there are many other ways to host your site for really cheap, something that's as cheap and reliable as the Heroku + GoDaddy combination will be hard to come by. Plus, one of the huge advantages of Heroku is that you can have an application that runs on various programming languages (Java, Ruby, Python, Node, and more).

**Important note:** For my own side projects, I utilize the free tier of [Cloudflare](https://www.cloudflare.com/), which enables me to take advantage of their CDN as well as the ability to have my sites on HTTPS for free. I'll write about this at some point in the future.
