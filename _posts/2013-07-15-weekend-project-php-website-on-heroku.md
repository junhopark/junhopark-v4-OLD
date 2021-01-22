---
layout: posts
---

I got hold of some really nice looking single page website templates earlier last week (from [here](http://www.mightydeals.com/deal/parallax-templates.html)) so I thought I'd go ahead and redo the website for my parents' shoe repair business.  I decided to host the site on Heroku (for free, of course).

This was my first PHP site running on Heroku and here are some things I learned along the way:

####index.php > home.html
I followed the advice of [this blogger](http://www.lemiffe.com/how-to-deploy-a-static-page-to-heroku-the-easy-way/) and...:

* Renamed **index.html** to **home.html**
* Created index.php which includes the following line: **<?php include_once("home.html"); ?>**

####Use SendGrid + SwiftMailer to send emails from the site
It turns out that Heroku does not support PHP's mail() function.  Thankfully, I can send emails through a SMTP server via the SendGrid add-on in Heroku.

I downloaded the PHP libraries for SendGrid from [here](https://github.com/sendgrid/sendgrid-php) and added the 'SendGrid Starter' (free) add-on via the Heroku dashboard.

In addition, I had to download the SwiftMailer PHP library from [here](http://swiftmailer.org/) and drop it into my project.  My PHP file looks like this:

    <?php
    require_once '../libs/swift-5.0.1/lib/swift_required.php';
    require '../libs/sendgrid-php/SendGrid_loader.php';
    $post = (!empty($_POST)) ? true : false;

    if ($post) {
        //...logic for email validation...
        $sendgrid = new SendGrid('SENDGRID-USERNAME', 'SENDGRID-PASSWORD');

        $mail = new SendGrid\Mail();
        $mail->addTo('SEND-TO-EMAIL-ADDRESS')->
            setFrom('FROM-EMAIL-ADDRESS')->
            setFromName('FROM-NAME')->
            setSubject('SUBJECT')->
            setText('PLAIN-TEXT-MESSAGE')->
            setHtml('HTML-MESSAGE');

        $sendgrid->smtp->send($mail);
    }
    ...

By the way, you can obtain your SendGrid username and password by executing the following commands in terminal:

    > heroku config:get SENDGRID_USERNAME
    > heroku config:get SENDGRID_PASSWORD

And just like I am doing with junhopark.com, I'm using the Zerigo DNS add-on to point the moodyshoerepair.com domain to my parents' shoe repair site.

Here are some screenshots of the new site:

![Moody Shoe Repair (new) - Home](/assets/img/moodyshoerepair_new_home_small.png)
![Moody Shoe Repair (new) - About](/assets/img/moodyshoerepair_new_about_small.png)
![Moody Shoe Repair (new) - Services](/assets/img/moodyshoerepair_new_services_small.png)
![Moody Shoe Repair (new) - Contact](/assets/img/moodyshoerepair_new_contact_small.png)

And screenshots of the old site:

![Moody Shoe Repair (old) - Home](/assets/img/moodyshoerepair_v3_home_small.png)
![Moody Shoe Repair (old) - Our Services](/assets/img/moodyshoerepair_v3_services_small.png)
![Moody Shoe Repair (old) - Find Us](/assets/img/moodyshoerepair_v3_findus_small.png)
![Moody Shoe Repair (old) - About Us](/assets/img/moodyshoerepair_v3_about_small.png)
![Moody Shoe Repair (old) - Contact Us](/assets/img/moodyshoerepair_v3_contact_small.png)

I'm really liking the look of the new site.  Glad I was able to find such nice looking templates for cheap.

**You can check out the new site by going to: [www.moodyshoerepair.com](http://www.moodyshoerepair.com)**
