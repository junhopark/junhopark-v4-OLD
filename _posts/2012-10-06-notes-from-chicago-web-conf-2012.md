---
layout: posts
---

Here are my notes from [ChicagoWebConf 2012](http://chicagowebconf.org/) (Oct 6, 2012).

#### A/B Testing Your Designs With Real Users - by Will Hacker (Cars.com)

* Big problem w/ In-lab & Guerilla UI testing is that you can only do this with a small group of people.  Statistically invalid.  
* A/B Testing: Multiple versions of a design tested on a live site & able to test large numbers of real users.  Statistically significant.  Fast to execute.  Can reduce team friction by letting users decide.  Design arguments are reduced.  Lets the users pick!
* A/B Cons: You learn "what" but not "why".
* Team friction: Different people w/ different opinions wanting different things.  Slows things down.  Time waster.  
* Amazon = known to be the king of A/B testing.  See what they do.
* Cars.com: Uses Optimizely.  
* A/B testing lets you discover small changes that can lead to huge improvements.
* You can also test multiple different screen flows with Optimizely.
* Alternatives to Optimizely: Adobe Test & Traget; Autonomy Optimost; Monetate TestLab; Webtrends Optimize
* Best practice is to first run Optimizely test on staging/testing server before running the test in production.

#### How to Build Web Apps Like Hollywood Makes Movies - by George DeMet

* Traditional "3 Acts" of building web dev projects: Discovery & Design > Development > QA
  * Good model for a **smaller project** (< 500 hours)
* Elements of a successful web platform
  * Builds on existing work done by a robust developer community.
  * Can be customized to meet specific use cases.
  * Can be added to and extended over time.
  * Can be used in non-obvious ways.
  * Delivers a consistent experience that meets user expectations.


#### HTML on Steroids - Angular.js - by Oren Golan (YP.com)

* Can get presentation from: github.com/oren
* A Google engineer started working on it 2008.
* Who's using it? DoubleClick; Good Films; Sony PS3's YouTube app; Colingo
* What?
  * Declarative
  * 2 way data binding
  * plain old JS objects
  * easy to test
* Very light-weight.

#### UX for Developers - by Pek Pongpaet (Firesnake Labs)

* pinstagram.co
* What is UX?
  * Balancing of: User Needs + Tech req's + Business objectives
* UX Lessons for developers
  * See what others have done.  Don't reinvent the wheel when you don't have to.
  * Check out: Mobile UI Patterns; Pattern Tap; Inspired UI
  * The low hanging fruit of UX is: Make it faster.  No one's gonna complain!
    * For every increase in +100ms = -1% in sales. (HUGE!)
  * Reduce friction.
    * For instance, make it super easy to sign up.  (for instance, not requiring users to type their passwords in twice)
    * Mockingbird: You don't need to create an account until you're trying to save your work.  Great idea.
  * Reduce inconsistency.  For instance, across different platforms.
  * Kill Features.
    * MS Word (too many features.  Or "features")
  * Sometimes you have to tell users what to do.
* Tools
  * Draw > Take a pic > Work on it.
  * FieldTest (fieldtestapp.com) - for building mobile prototypes


## Action items (listed in priority)

* What are some ways to reduce "friction" on Cappex.com?
* Check out angular.js
* Look into Optimizely.
* Look into how Amazon does A/B testing.
