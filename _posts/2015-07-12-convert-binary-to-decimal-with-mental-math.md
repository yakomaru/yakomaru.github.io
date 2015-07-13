---
title:  "convert binary to decimal with mental math"
date:   2015-07-12 17:00:00
categories: tricks
---

A tutorial on how to convert binary numbers in your head.


**Usefulness**

While this skill isn't terribly useful, since a quick Google search will list several sites which
can perform the conversion for you, it has been known to show up in technical interview questions and
it's pretty impressive to people who don't understand how it works.

**How it works**

The general idea is to move from the left side of the number to the right. Every time you shift,
multiply your running total by 2, and when you hit a 1, add it to your total.

Example:

{% highlight plain %}

101010
^ start with 1 (total = 1)
101010
 ^ shift to the right means multiply by 2, 
 the digit is 0 so don't add anything (total = 2)
101010
  ^ shift again, multiply by 2, and then add 1 
  because there's a 1 here (total = 5)
101010
   ^ another shift, multiply by 2 (total = 10)
101010
    ^ another shift and a 1 so multiply by 2 and 
    add 1 (total = 21)
101010
     ^ last shift, multiply by 2 and we're done 
     (total = 42)

{% endhighlight %}

**Working with fractions**

Converting binary fractions is a bit harder but follows a similar pattern. The difference here
is the starting point is the right side and the end is the ones place. Also, we divide by 2 instead
of multiplying by 2 as we shift.

Example:

{% highlight plain %}

0.101
    ^ start with 1 (total = 1)
0.101
   ^ divide by 2 (total = 0.5)
0.101
  ^ divide by 2 then add 1 (total = 1.25)
0.101
^ divide by 2 and we're done (total = 0.625)

{% endhighlight %}

**External resources**

[Exploring Binary: Binary Converter](http://www.exploringbinary.com/binary-converter/) You can use this if you want to test yourself.