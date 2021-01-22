---
layout: posts
---

I decided to conduct some simple page load speed testing.  I hope the following info might be of some value to some folks out there.

## What did I want to measure?
* Page load speed when JavaScript and CSS stylesheets are bundled Vs. when they are unbundled.
* Page load speed while the page is being loaded while utilizing CloudFlare Vs. not utilizing CloudFlare.

## Pages I set up to conduct my test:
* [/http2-test-with-unbundled-resources](https://junhopark.com/http2-test-with-unbundled-resources): Very simple page consisting of 80 unbundled CSS files and 80 unbundled JavaScript files.  Each of these files are 120,000 bytes in size totaling 19,200,000 bytes.
* [/http2-test-with-bundled-resources](https://junhopark.com/http2-test-with-bundled-resources): Very simple page consisting of 1 bundled CSS file and 1 bundled JavaScript file.  Each of these files are 9,600,000 bytes in size totaling 19,200,000 bytes (120,000 x 80 = 9,600,000).

## Conditions under which testing was completed.
* Chrome was the browser of choice for testing.
* I tested on OS X that has a hardwired Ethernet connection.
* The connection speed was throttled to 4 Mbps using Chrome Developer Tools.
* I disabled browser cache by having selected the "Disable cache" checkbox in Chrome Developer Tools.
* When pages were loaded utilizing CloudFlare, they were loaded in HTTP/2 instead of HTTP/1.1.
* When pages were loaded utilizing CloudFlare, there was some significant optimization happening thanks to its CDN infrastructure.

## What were the results?
* [https://junhopark.com/http2-test-with-unbundled-resources](https://junhopark.com/http2-test-with-unbundled-resources) (Utilizing CloudFlare)
    * Average after 10 page loads (in seconds): Finish: 2.153 | DOMContentLoaded: 2.242 | Load: 2.241
* [https://junhopark.com/http2-test-with-bundled-resources](https://junhopark.com/http2-test-with-bundled-resources) (Utilizing CloudFlare)
    * Average after 10 page loads (in seconds): Finish: 1.0678 | DOMContentLoaded: 1.326 | Load: 1.343
* [http://junhopark.herokuapp.com/http2-test-with-unbundled-resources](http://junhopark.herokuapp.com/http2-test-with-unbundled-resources) (NOT Utilizing CloudFlare)
    * Average after 5 page loads (in seconds): Finish: 38.22 | DOMContentLoaded: 38.094 | Load: 38.094
* [http://junhopark.herokuapp.com/http2-test-with-bundled-resources](http://junhopark.herokuapp.com/http2-test-with-bundled-resources) (NOT Utilizing CloudFlare)
    * Average after 5 page loads (in seconds): Finish: 38.094 | DOMContentLoaded: 37.976 | Load: 37.976

## Conclusion & thoughts
* CloudFlare significantly improved page load performance (1 - 2 seconds Vs. 38 seconds!!!)
* When pages are loaded via CloudFlare, bundling of resources can drastically improve page load speed.
* I wonder how my testing would be impacted if...:
    * In addition to CSS & JavaScript files, I were to include images.
    * I were to load less/more unbundled resources.
