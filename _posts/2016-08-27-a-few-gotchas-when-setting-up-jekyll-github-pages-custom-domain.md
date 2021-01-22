---
title: A few gotchas when setting up Jekyll + GitHub Pages + custom domain
layout: posts
---

I just finished "converting" my music website from Heroku to utilizing [Jekyll](http://jekyllrb.com/) + [GitHub Pages](https://pages.github.com/).  And by "converting", I mean I killed off a project that was set up using Ruby on Rails and decided to set up an entirely new site with a completely different look & feel (rather ugly before and rather ugly now, I know...) built using Jekyll and GitHub Pages.  I did this because I wanted to start writing blog posts on my music site and the existing site wasn't really set up for me to write blog posts on.  Plus, I wanted to give Jekyll a try.

The initial setup was extremely easy and I'm not going to go through that because the [documentation that's up on GitHub](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) is more than sufficient and very easy to follow if what you care about is getting a Jekyll site using the default theme ("Minima") without any sort of layout customization.  However, I did run into some gotchas when I attempted to apply even the simplest of customizations.  Here are the 2 main gotchas I ran into:

## Gotcha #1: Customizing the page layout
It took me a while to figure out how to update the page layout, such as the header and the footer.  All of my Googling efforts told me that I needed to update files inside of the *_includes* folder which is inside the root of my project; however, I simply did not see this folder.  I thought I had lost my mind (it's entirely possible when you have 2 little kids at home) so I set up a new Jekyll project from scratch.  Still no *_includes* folder.  After even more Googling, it seemed to me that at some point in Jekyll's history they moved to encouraging people to use Gem-based themes and in this model, the theme-specific files are no longer included in the project that you create.

I'm sure there are multiple ways to solve for this but here's what I did to customize the *\<head\>...\</head\>* section of my project:

* I created an *_includes* folder at the root of my Jekyll project.
* Inside of the *_includes* folder, I created a *head.html* file, which is intended to override the *_includes/head.html* file that's included in the [Minima theme](https://github.com/jekyll/minima).
* FYI - this is what I had to do to get Google Analytics set up (Google Analytics requires that I include a code snippet inside of *\<head\>...\</head\>*.

## Gotcha #2: Setting up a custom domain
I set up my project as a GitHub "project" Page (as opposed to an organization page) because I wanted to be able to set up multiple GitHub Pages sites in the future under a single GitHub account ([See here](https://help.github.com/articles/user-organization-and-project-pages/) for an explanation on User, Organization, and Project Pages).  What this meant was that in my *_config.yml* file, the *baseurl* variable was set to *"/junhoparkmusic-v2"*.  Everything was loading correctly both locally (via *http://localhost:4000/junhoparkmusic-v2*) as well as on GitHub (via *junhopark.github.io/junhoparkmusic-v2*).  However, as soon as I set up a custom domain (*junhoparkmusic.com*) things started breaking.  When I went to [junhoparkmusic.com](https://junhoparkmusic.com/), I could see that it was hitting GitHub but the rendering was all messed up.  Again, I'm sure there are multiple ways to solve for this but here's what I did to fix it:

* In *_config.yml*, I set the *baseurl* variable to be an empty string (ie, *baseurl: ""*)
* I confirmed that my site was loading correctly both locally (via *http://localhost:4000*) as well as on GitHub (via *https://junhoparkmusic.com*).

Here's the site: [https://junhoparkmusic.com](https://junhoparkmusic.com)

And the source on GitHub: [https://github.com/junhopark/junhoparkmusic-v2](https://github.com/junhopark/junhoparkmusic-v2)
