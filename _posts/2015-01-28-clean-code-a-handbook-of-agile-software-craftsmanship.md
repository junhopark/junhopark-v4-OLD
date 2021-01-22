---
layout: posts
---

Something I'd like to start doing in 2015 is to write a blog post after finishing a book, provided that there are at least a few key takeaways.  I'm thinking that doing this will help me process the book at a deeper level and help me get more out of reading books.  I want the books that I read to make a visible impact in my life and I think writing mini "book report" blog posts will help me accomplish that.  I'm currently in the midst trying out <a href="https://www.safaribooksonline.com/" target="_blank">Safari Books Online</a> and the very first book I decided to read was a book that I've had on my Amazon Wish List for a very long time: **Clean Code: A Handbook of Agile Software Craftsmanship written by <a href="https://twitter.com/unclebobmartin" target="_blank">Uncle Bob</a>**.

Anyhow, here's a list of what I consider to be the most important takeaways for me:

* **Write code that clearly communicates its intent.**  Be as clear and explicit as possible without being overly verbose.  I need to make it as easy as possible for people to understand my code.  If I have a difficult time understanding my own code (or I'm not 100% certain why it works), I should pretty much guarantee that others who read my code will have an even more difficult time.

* **Functions should do ONE thing.**  This was stressed throughout the book and I really needed this reminder.  While I'm usually mindful of keeping my functions short and concise, I don't do as good of a job ensuring that my functions do only 1 thing and that there are no side effects in my functions.

* **Pay attention to vertical ordering of functions in a source code file.**  I don't remember ever reading about (or thinking about) this before.  In the book it talks about how "function call dependencies [should] point in the downward direction" and I agree that this does make the code more readable.  In the same paragraph, the author talks about how the most important concepts of the source code should be placed at the top and low-level details should be placed at the bottom.  This is something I will keep in mind as I write code.

* **Write unit tests to learn library code that I don't understand.**  This is another new concept that I had never heard of before.  The author talks about writing unit tests to help me understand library code and talks about how once these unit tests are written, they can be run when the library code needs to be updated to help me understand any behavioral differences between the old Vs. new library code.  This is a really neat concept.

* **Remember Kent Beck's 4 rules of Simple Design.**  In chapter 12, it talks about Kent Beck's 4 rules of Simple Design, which are: 1) Runs all the tests. 2) Contains no duplication. 3) Expresses the intent of the programmer. 4) Minimizes the number of classes and methods.  I like lists and I like this one.

* **When writing concurrent code, keep synchronized sections small.**  I'm going to copy & paste the section that really stood out to me: "The synchronized keyword introduces a lock. All sections of code guarded by the same lock are guaranteed to have only one thread executing through them at any given time. Locks are expensive because they create delays and add overhead. So we don't want to litter our code with synchronized statements" (Chapter 13).

* **Run with more threads than cores.** Here's another helpful bit related to writing concurrent code: "Things happen when the system switches between tasks. To encourage task swapping, run with more threads than processors or cores. The more frequently your tasks swap, the more likely you'll encounter code that is missing a critical section or causes deadlock" (Chapter 13).

I liked that the book was full of practical concepts.  And I know a lot of people would probably complain about this, but I (being that I spend a lot of my time writing Java code) liked that the book was very much Java-centric.

My overall verdict on this book: **Thumbs Up**
