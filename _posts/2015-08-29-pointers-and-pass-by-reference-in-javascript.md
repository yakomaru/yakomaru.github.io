---
title:  "pointers and pass by reference in javascript"
date:   2015-08-29 13:30:00
categories: javascript
---

An explanation of how Javascript efficiently passes large data.


**Where are the pointers?**

When I first started using Javascript I noticed that it lacked a pointer data type. Coming from 
other languages, I wondered how Javascript passed large data types like objects and arrays. So I 
did some experimentation and discovered that whenever an object is stored to a variable, that 
variable becomes a pointer to the object instead of the object itself.

Here's an example:

{% highlight javascript %}

var pointer1 = {a: 1};
var pointer2 = pointer1;

pointer1.a++;
console.log(pointer1, pointer2); // both are now {a: 2}

{% endhighlight %}

Note that when either variable pointer1 or pointer2 change, the shared object they point to in 
memory changes.

Pointers can also be stored in objects:

{% highlight javascript %}

var obj = {value: null};
obj.value = obj;

console.log(obj); // {value: {value: {value: ...}}} and so on

{% endhighlight %}

In this case the property value in obj contains a pointer to it's own object which means when 
attempting to log it the nested objects never end.

**Passing Arrays**

Because variables for objects and arrays (which are really just objects in Javascript) are all 
pointers. When passing an array into a function, the function will have a pointer to the original 
array. This means any changes to the array within the function will also change the array outside 
the function.

Example:

{% highlight javascript %}

var arr = [1, 2, 3];
var func = function(array) {
  for(var i = 0; i < array.length; i++) {
    array[i]++;
  }
};

func(arr);
console.log(arr); // [2, 3, 4]

{% endhighlight %}

Note that the original array is modified instead of a copy of the array being made within the function. 
To avoid modifying the original array, a copy of the array should be made before any modifications:

{% highlight javascript %}

var arr = [1, 2, 3];
var func = function(array) {
  array = array.slice();
  for(var i = 0; i < array.length; i++) {
    array[i]++;
  }
  return array;
};

console.log(func(arr)); // [2, 3, 4]
console.log(arr); // [1, 2, 3]

{% endhighlight %}

Here the array is copied using the slice() function so the original array stayes the same.

**One last example**

Here's one last example that shows some of the interesting things that can be done with pointers:

{% highlight javascript %}

var obj = {value: null};
obj.value = obj;

console.log(obj); // {value: {value: {value: ...}}} and so on

{% endhighlight %}

In this case the property value in obj contains a pointer to it's own object which means when 
attempting to log it the nested objects never end.
