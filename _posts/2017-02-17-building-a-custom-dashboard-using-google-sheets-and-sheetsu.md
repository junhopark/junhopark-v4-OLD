---
layout: posts
---

I was looking for a way to build a custom dashboard that's relevant for me and the team (especially my DevOps team), which at the very least, includes the following information:

* Frequency of errors and exceptions occurring in application logs in production
* Number of open bugs in Jira

Not only did I want this dashboard to reflect how things are currently but also what the trend is.  I didn't need anything that looks pretty or fancy.  I just needed to see the numbers I care about and some sort of an easy-to-read graph.

I spent some time on Google looking for "custom dashboard" solutions.  After taking a look at a few options (commercial as well as open source) I decided to keep it simple and build my own solution utilizing Google Sheets.  I decided on this for the following reasons:
* All I cared about at the end of the day was to be able to keep track of a few numbers and see a simple visual graph that represents these numbers.  Google Sheets can certainly do this.
* I had a feeling that whichever "custom dashboard" tool I pick would require decent amount of upfront work to configure it initially.  I wanted to try to get something up and running quickly.
* We already use Google Sheets on my team and if I can get what I want using an existing tool (Vs. introducing a new tool) that is always my preference.  There are always overhead costs associated with introducing new tools to the team.
* I wanted to be able to own whatever data gets fed into this custom dashboard tool.  I'm reasonably confident that Google Sheets will be around for a very long time.  Plus, I can always easily export this data to an Excel format (also pretty confident Excel will be around for awhile).

Once I decided to leverage Google Sheets for this, I figured I'll set up a job in Jenkins to be kicked off once a day > Get the numbers I want from my various sources (eg, application log repository & Jira) > Send over these numbers to Google Sheets using their API.

I spent a little bit of time playing around with Google's API and realized I was not going to be able to get it up and running in 5 minutes.  So I spent a little bit of time Googling and came across a solution called [Sheetsu](sheetsu.com).  From looking at the product description, it looked crazy easy to use and it proved to be true.  I was able to start posting data to a Google Sheet document within minutes of signing up for Sheetsu.  Pretty sweet!  The way that Sheetsu is able to handle data updates to Google Sheets is absolutely fantastic from an ease-of-use standpoint.  I'm able to add data to my Google Sheet document by doing *curl* against a Sheetsu endpoint (which is associated with my Google Sheet document).

Fast forward 5 months since when I initially set up this "dashboard" - and it's been serving me well.  Because Sheetsu is so easy to use, it's been a breeze for me to add new data points to my dashboard.  I have multiple worksheets inside a single "Cappex Engineering Metrics" document and if I want to add new data points to my dashboard, it's as easy as adding a new worksheet and updating or adding a Jenkins job to make a *curl* call against a Sheetsu endpoint.
