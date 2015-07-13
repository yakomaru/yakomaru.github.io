---
title:  "why use higher-order functions?"
date:   2015-07-12 12:00:00
categories: javascript
---

An argument for increased higher-order function usage to improve readability and debugging.


**More concise code**

Consider the following examples in English:

>I ***went*** to the city.
>
>I ***drove*** to the city.

Note that ***went*** can be used in more cases than ***drove***. However, ***drove***
more accurately describes how I got to the city. ***Drove*** is the more concise version
of ***went***.

Now consider a similar example in javascript:

{% highlight javascript %}
var array = [1, 2, 3];

for(var i = 0; i < array.length; i++) {
  //code
} // -> ???

array.some(function(element) {
  //code
}); // -> true/false

{% endhighlight %}

Similarly, the for loop is more versatile and can perform the same operation as the some()
function below it, but its versatility is also a drawback because we don't know what it
will do until we study the code within its curly brackets. The some() function is much more
descriptive as it will always iterate over the array and return true or false depending on 
if any of the array's elements pass a truth test.

The takeaway here is that higher-order functions are much clearer than their low-level equivalents.

**Standard inputs and outputs**

Higher-order functions wrap low-level code within an appropriately named function
with the goal of standardizing the inputs and outputs.

For example:

{% highlight javascript %}
var array = [1, 2, 3];
var callback = function(element) {
  return element + 1;
}

array.map(callback); // -> [2, 3, 4]

{% endhighlight %}

The higher-order function map takes an array and a callback function
as input and performs the callback on every element of the array. Map then returns
a new array with the results of the operation.

The important thing to note in this example is that map will always return an array
and that array will always have the same number of elements as the array passed into
it. The input and output for map is standardized to these constraints so that no surprises
come out of it. 

**Conclusion**

Higher-order functions offer some great readability benefits at only a slight cost to
the call stack and run time. The main difficulty with them involves learing what
each one does. Much like expanding your vocabulary in English, expanding your higher
order function vocabulary in Javascript takes time, but the benefits are well worth it.

**External resources**

[Eloquent Javascript Chapter 5: Higher-Order Functions](http://eloquentjavascript.net/05_higher_order.html)