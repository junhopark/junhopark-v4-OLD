---
layout: posts
---

I recently had a need to write a simple script that writes to a Google Sheet document once a day. I decided to write the script in Ruby and host it on Heroku since I didn't want my laptop to be on in order for the script to run. After spending some time Googling & some trial and error, I came up with something that works and is quite simple. For the purposes of this blog post, I will write a Ruby script that accesses a newly created Google Sheet document and does the following:

* Prints out to the console how many rows are contained in the Google Sheet document
* Adds the current date & time to a new row in the document

I will then set up a recurring job on Heroku to execute the script every 10 minutes.

## The Steps

Create a new Google Sheet document.

Create a new project in Heroku. For the purposes of this example, I'm calling it: *scheduled-ruby-script*

If you haven't already, install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli). After it's been installed, set up your project locally:

    $ heroku login
    $ mkdir scheduled-ruby-script
    $ cd scheduled-ruby-script
    $ git init
    $ heroku git:remote -a scheduled-ruby-script

At the project root, create a Gemfile with the following 2 lines in the file:

    source "https://rubygems.org"
    gem "google_drive"

Let's go ahead and create the Ruby script. We're going to utilize the [Google Drive Ruby Gem](https://github.com/gimite/google-drive-ruby). Let's call the file *script.rb* and it should contain the following. **NOTE:** When you're setting the *google\_sheet\_id* variable below, this comes out of the Google Sheet document's URL. This is the unique identifier looking thingie part of the URL. For example, if the URL is *https://docs.google.com/spreadsheets/d/1iB6vU90eFVjLa93jyb4TdT2fArNddXWQSEnFRamerA7/edit#gid=0* then you should set the variable to: *"1iB6vU90eFVjLa93jyb4TdT2fArNddXWQSEnFRamerA7"*

    require "google_drive"

    session = GoogleDrive::Session.from_config("config.json")

    # You can grab this from the URL of the Google Sheet document
    google_sheet_id = "[SEE MY NOTE ABOVE!]"

    ws = session.spreadsheet_by_key(google_sheet_id).worksheets[0]

    ws[ws.num_rows + 1, 1] = Time.now

    ws.save

    # Reloads the worksheet to get changes by other clients.
    ws.reload

    p "Number of rows in the Google Sheet document: #{ws.num_rows}"

Let’s test the script locally.  

    $ bundle install
    $ ruby script.rb

When you run the script for the first time, you'll be asked to go to a URL that starts with *https://accounts.google.com*. Go to the URL in your browser and copy the code that you're provided with. Paste that back in your Terminal and press return. This will create a *config.json* file at the project root and it contains the credentials that allows your script to access to the Google Sheet document.

If your script runs successfully, you should see something like *"Number of rows in the Google Sheet document: 1"* printed out in the Terminal and see a timestamp in the Google Sheet document.

![](/assets/img/ruby-heroku-google-sheets/1_record.png)

Once you've confirmed that the script is working locally, let's commit your files and push them up to Heroku.

    $ git add .
    $ git commit -m “Writes to Google Sheet document and reads from it"
    $ git push heroku master

Once the files are pushed up, let's test it on Heroku.

    $ heroku run bash
    Running bash on ⬢ scheduled-ruby-script... up, run.5080 (Free)
    ~ $ ruby script.rb
    "Number of rows in the Google Sheet document: 2"

And if you look at the Google Sheet document, you should see that another timestamp has been added. Note that when the script runs on Heroku, the timestamp will be in UTC.

Now, if we want *script.rb* to be executed every 10 minutes, you'll need to configure Heroku Scheduler. Go to: [https://dashboard.heroku.com/apps](https://dashboard.heroku.com/apps) > Select your application (eg, *scheduled-ruby-script*) > Click on *Configure Add-ons*.

![](/assets/img/ruby-heroku-google-sheets/add_ons.png)

Under *Add-ons* > Type in: *Heroku Scheduler* > Select the *Provision* button. You should now see that the Heroku Scheduler add-on has been added. Click on the *Heroku Scheduler* link.

![](/assets/img/ruby-heroku-google-sheets/heroku_scheduler.png)

Click on 'Add new job' and update the fields to have *ruby script.rb* run *Every 10 minutes*. Select the *Save* button.

![](/assets/img/ruby-heroku-google-sheets/new_job.png)

Give it some time (< 10 minutes) and if everything works, you should eventually see a new record get added to your Google Sheet document.
