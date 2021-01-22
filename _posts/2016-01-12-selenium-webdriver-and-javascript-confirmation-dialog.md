---
layout: posts
---

One of many things I had been wanting to accomplish in the 2nd half of 2015 was to start making some hands-on contributions to my team's functional test automation code, which utilizes Selenium WebDriver.  I'm a firm believer that in order to be an effective technical manager, you need to have a certain level of technical expertise.  During my 3 and a half years that I've been at Cappex.com, I've had little-to-no experience working on the test automation code (well, it didn't even exist until about a year after I joined the company) and as such, I had felt that there's very little that I can do to technically support my QA manager and QA engineer.  So anyhow, sometime late last year I decided I would make my first significant contribution to our test automation code.

I spent a few hours writing my test, which involved the following set of actions:

* User logs in
* The user is then shown a list of other users whom he/she can log in as.  Think of a manager who can log into her direct reports' accounts.  Or, a teacher who can log into his students' accounts.
* When the user decides to log in as another user, say, User X--the user clicks on the 'User X' hyperlink.
* And when the 'User X' hyperlink is clicked, you are shown a JavaScript confirmation dialog that says something to the effect of "You are logging in as another user.  Are you sure you want to do this?"
* When the user selects the OK button, then the user is logged in as User X.

Pretty straight forward, I thought.  Well, I ended up spending several hours dealing with selecting the OK button inside of the JavaScript dialog.  The problem was that when WebDriver opened up the JavaScript confirmation dialog, the dialog closed on its own a split second after it was opened up--without either the Cancel or the OK button being clicked.  The code looked like this:

    WebElement loginAsUserLink = driver.findElement(By.cssSelector("div[data-userid='" + userId + "'] .loginAsUser"));
    loginAsUserLink.click();
    (new WebDriverWait(selenium, 2)).until(ExpectedConditions.alertIsPresent());
    Alert alert = selenium.switchTo().alert();
    alert.accept();

After a long time Googling around for a solution as well as debugging through my code multiple times, I was still unable to resolve the issue.  And then I thought to myself, "hm, I wonder what would happen if, instead of having WebDriver click on the 'User X' hyperlink, I were to press the enter key on the hyperlink".  So I updated my code as follows:

    WebElement loginAsUserLink = driver.findElement(By.cssSelector("div[data-userid='" + userId + "'] .loginAsUser"));
    loginAsUserLink.sendKeys(Keys.ENTER);
    (new WebDriverWait(selenium, 2)).until(ExpectedConditions.alertIsPresent());
    Alert alert = selenium.switchTo().alert();
    alert.accept();

And that fixed it!  It still does not make sense to me whatsoever that clicking the 'User X' hyperlink would make the JavaScript dialog disappear without waiting for the Cancel/OK button selection.
