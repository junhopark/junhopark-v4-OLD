---
layout: posts
---

I upgraded both my MacBook Air and MacBook Pro to Yosemite over the weekend and I saw that both my laptops were unable to connect to internal systems at the office.  For instance, I wasn't able to access my QA server by going to *http://qa.cappex.local*.  I, however, was able to access the same server by going to *http://qa/*.  Also, I saw that while I wasn't able to ping qa.cappex.local, nslookup worked just fine.

I Googled around for a good 20-30 minutes in search of a fix to this problem and came across an answer in [https://discussions.apple.com/thread/6611817](https://discussions.apple.com/thread/6611817).

Executing the following command in my terminal resolved the DNS issue on both my Macs:

    sudo discoveryutil mdnsactivedirectory yes

Problem solved.
