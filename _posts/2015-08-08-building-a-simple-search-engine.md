---
title:  "building a simple search engine"
date:   2015-08-08 16:30:00
categories: javascript angular jquery node
---

A brief overview of some of the challenges I faced while making a search engine.


**Introduction**

I recently built an application I like to call Inquiry. Inquiry accepts a webpage as input,
which it then parses for links and keywords. After obtaining all the links on the original page, 
Inquiry then requests the pages at those links and parses them for keywords. The end goal is to
build an object filled with pages and associated keywords which can then be filtered with
Angular.

To see it in action, check out [Inquiry](http://inquiry-search.heroku.com) or host it locally by
downloading the repository from [GitHub](https://github.com/yakomaru/inquiry).

**CORS Requests**

I initially planned to make this application 100% front-end without the need for a server. This 
was my first mistake, thanks to the same origin policy. The same origin policy states that
http requests from scripts can only be made to the domain they originate from. This means my
front-end search engine had no way of making http requests to outside web pages.

There are a few ways to solve this issue, but I ultimately chose to bite the bullet and build
a simple server. The addition of a server allowed for my application to make requests to the server 
instead. The server can then make unrestricted requests to other web pages and then return the 
obtained html file as a string to the application.

**Manually Updating the Angular View**

Another issue I faced involved an Angular specific problem. For the most part, Angular is very
good at updating the view when the user interacts with the page, but I found it isn't as good
at keeping track of changing objects on the back-end. An easy way to force Angular to update
is to call `$scope.$apply()` within the controller.

**Using JQuery on HTML Data**

After grabbing html data from a given website, I was faced with the challenge of parsing out
the links and keywords. JQuery makes this task easy, but how can you use JQuery on a string? 
Luckily I stumbled upon the [DOM parser](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser). 
The DOM parser allowed me to parse the stringified html into a DOM object which can then be 
easily passed to JQuery with `$('a', domObj)` to find all the anchor tags. JQuery then has the ability 
to pull out links or text from each tag.

**Conclusion**

Building this application was a great experience for me and I feel like I learned a lot from it.
May the knowledge I gained help the rest of you.
