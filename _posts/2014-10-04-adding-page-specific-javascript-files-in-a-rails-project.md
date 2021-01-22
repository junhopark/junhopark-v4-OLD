---
layout: posts
---

Being that I'm a Ruby on Rails newbie, I was looking for a way to add page-specific JavaScript files on a Ruby on Rails (Rails 4) project.  Here's one way to accomplish this and I think it makes sense & keeps things simple & clean.

### app/assets/javascripts/application.js
Add the following line:

	require_directory .

And delete the following line if it exists:

	require_tree .

### app/assets/javascripts/
Include all of your application-wide JavaScript files in the _app/assets/javascripts_ directory.  Inside of this directory, create a subdirectory which will include all of your page-specific JavaScript files.  It's probably best if the name of this subdirectory correlates with the name of the page.  For instance, if you've got an "About" page, name the subdirectory _about_.

### app/assets/javascripts/about/
Inside of this directory, create your page-specific JavaScript file.  Let's keep it simple and name it _about.js_.  In addition, you can move all of your page-specific JavaScript files into this folder.

### app/assets/javascripts/about/about.js
At the very top of this file, include the following line:

	//= require_directory .

### app/views/pages/about.html.erb
Somewhere in this page, adding the following line will cause all of the JavaScript files inside of the _app/assets/javascripts/about/_ to be included on the "About" page only.

	<%%= javascript_include_tag "resume/resume.js" %>
