---
layout: posts
---

As I noted in my blog post from 9/15, I decided to recreate my site using Ruby on Rails + Postmarkdown and deploy to Heroku.  FYI, my site is a super simple single-page site with a blog.

__NOTE:__ I'm running: Ruby 1.9.3 + Rails 3.2.8 on OS X (MacBook Air 2012)

Here are the steps I took in making this happen:

* Installed Postgres locally.  I did this since projects created in Rails 3 uses SQLite by default, which Heroku does not like.  Heroku does like Postgres, however.
* I created 3 Postgres databases locally.  One for dev, one for test, and one for production.  These are the 3 databases that Rails expects when creating a new project.
* I created a new Rails project by running the following command: _rails new junhopark --database=postgresql_ This creates a new Rails project and uses Postgres instead of SQLite.
* My site contains a single 'home' page.  I ran the following command to create a _Pages_ controller with a single action (_home_):  _rails generate controller Pages home_
* I ran the following commands to create a local Git repository and commit my project:  _git init_ > _git add ._ > _git commit -m 'Initial commit'_  __NOTE:__ I soon learned about GitX, which is a nice (and free) Git GUI app on OS X.  Since my initial project commit, I've been using GitX to meet most of my Git needs.
* Create a Heroku project and push my code:  _heroku create_ > _git push heroku master_
* Updated _app/views/pages/home.html.erb_ to make my site (i.e. the 1 page on my site) look the way I want it to. (Basically what you see when you go to [junhopark.com](http://www.junhopark.com "junhopark.com").)
* In _config/routes.rb_, deleted _get "pages/home"_ and added _root :to => 'pages#home'_  This basically tells Rails that whenever someone goes to the root of the project (i.e. www.junhopark.com/) Rails should execute the _Pages_ controller and call the _home_ action.
* Updated all of the Rails provided error pages (such as 500.html, 404.html, etc.) in the _public_ folder.
* Added _public/errorstylesheet.css_ which is used only for the error pages.  I'm thinking that there's a better way to do this (and I'm sure there are many different ways of doing this) but this is the way I found that worked for me.  Note that in order to test that the error pages are coming up correcty, you need to run your Rails server in production mode.
* I'm forgetting why I had to do this, but at some point during my development cycle, I updated _config/environments/production.rb_ and set _config.serve_static_assets_ as well as _config.assets.compile_ to _true_.
* Pushed my changes to Heroku and checked that everything is working as expected.
* Added [Postmarkdown](https://github.com/ennova/postmarkdown "Postmarkdown on GitHub") to my project.  Updated _Gemfile_ by including the following line: _gem 'postmarkdown'_
* Ran _bundle install_ > _rails generate postmarkdown:install_
* Made use of Postmarkdown-provided theme.
  * Ran the following command: _rails generate postmarkdown:override --theme_  __NOTE:__ For some odd reason, when I ran this command, _views/layouts/postmarkdown.html.haml_ was created in my project root.  I moved _postmarkdown.html.haml_ file into _app/views/layouts_ and deleted the _views/layouts_ directories that were created.
  * Created the following file: _/config/initializers/postmarkdown.rb_ and inserted the following line: _Postmarkdown::Config.options[:use_theme] = true_
* Restarted Rails server to see changes take into effect
* Updated _postmarkdown.html.haml_ to update styling in Postmarkdown pages.
* Created new blog post entries by running the following command: _rails generate postmarkdown:post __name-of-post__ --date=__2012-09-16___
* Committed changes to Git and pushed changes to Heroku.

The end.
