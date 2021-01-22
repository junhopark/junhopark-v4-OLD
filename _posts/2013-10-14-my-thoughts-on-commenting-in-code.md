---
layout: posts
---

A skill that is often overlooked amongst developers and development managers is the ability to write good comments in code, which is understandable I suppose.  Comments don't (directly) cause bugs in software.  Comments aren't necessary in the same way that code is necessary in order to make software function.  And while many developers are often reviewed and critiqued on their ability to write good code, most developers and development managers (at least the ones I've worked for/with) don't care nearly enough about the comments that developers add to the code.  In my computer science studies during college, I don't remember a whole lot of emphasis being placed upon writing good comments.  I certainly don't remember any lectures or quizzes dedicated to teaching students how to write good comments in code.

Having said that, I think most developers would agree that writing good comments is a good skill for developers to possess.  They're necessary because comments can explain things that simply cannot be explained just by reading the code (such as business rationale and addressing *why* something was written a certain way).  They're necessary when you're working with legacy code that's extremely difficult to decipher and refactoring it to be more readable would take you way too long (not to mention the fact that you'll most likely end up creating new bugs).  Hence, you make your slightly hacky coding changes as best as you can and then add a few lines of comments to explain it.

So, in my attempt to write better comments, I thought I'd put together a list of what I'd consider to be good practices when it comes to commenting in code.

**1. Do not explain the obvious:** Don't add comments for lines of code that can be understood by simply reading the code.  This means no comments for things such as variable declarations as well as straightforward getters & setters.  I've gotten in the habit of deleting such comments when I come across them.

**2. Do explain the not-so-obvious:** The following should be candidates for inclusion in your comments:  Business rationale, edge cases, acceptable ranges for parameters.

**3. Write method-level & class-level comments:**  Summarize and explain what the method/class does, unless it breaks Rule #1.  I should have a reasonable understanding of what the class/method does by looking at the class/method name, its parameters (for methods), and class/method-level comments.

**4. No comments for obvious parameters:** When writing method-level comments, don't include comments for parameters that are dead obvious.  I supposed the only exception to this would be if you need to publish comments for all publicly-accessible methods and you were required to list all parameters no matter how obvious they are.

**5. Do not turn obsolete lines of code into comments:**  I see this practice pretty often--whereby developers will comment out lines of unnecessary code and then right above it, add something to the effect of ***//This code is no longer necessary***.  Just delete those lines, please, and remember that we can safely rely on VCS to bring deleted code back to life.  I've also gotten in the habit of deleting obsolete code that's been commented out.

**6. Keep comments up-to-date:** If the code you're changing has comments associated with it, make sure to review check the comments and make any necessary any adjustments to the comments.  Out of date comments are often worse than no comments in that they cause confusion.

**7. Write comments in unit tests:** Remember that comments are helpful for unit tests as well.  I will admit that I often forget to do this myself.

**8. Comments are not substitutes for poorly written code:** It can be tempting to write code in a hurry (often hindering readability and testability) and add comments to make up for it.  While there are times when this is unavoidable, avoid doing this *whenever possible*.  If you willingly write code that's difficult to read and attempt to make up for it by attaching comments to it, spend some time and ask yourself if the code can be refactored or re-written to make comments unnecessary.  Developers who end up inheriting your code will love you for it.
