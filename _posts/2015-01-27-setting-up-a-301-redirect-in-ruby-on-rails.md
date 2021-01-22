---
layout: posts
---

I saw in Google Analytics that I've been getting a lot of hits on junhopark.com/index.php, which isn't a valid page.  I decided that it'd be best to set up a 301 permanent redirect from /index.php to /.

My guess was that setting up this redirect would involve making a change to routes.rb (I was right) but I wasn't quite sure about the syntax (yep, I'm a rails newbie).  I started Googling, thinking that I would come up with the answer in a minute.  Well, perhaps my Googling skills are terrible, but it took me significantly longer than a minute to come up with the answer.

Well, here's the solution:

    get '/index.php', to: redirect('/')

Duh.
