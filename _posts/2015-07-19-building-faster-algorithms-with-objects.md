---
title:  "building faster algorithms with objects"
date:   2015-07-19 18:30:00
categories: javascript
---

A guide on how to use storage objects instead of nested loops for faster array and string
manipulation.


**Consider this problem**

Let's say we need to perform some statistical calculations on an array of data. One requirement
might be to find the mode of a given data set. The mode of a given set of numbers is the number
repeated most.

For the sake of simplicity, let's assume that the data set only has one mode. A naive approach
to solving the problem might be to use nested loops to compare each number with the rest of
the array and count up the number of times it repeats.

{% highlight javascript %}

var nestedMode = function(array) {
  var highest = 0;

  for(var i = 0; i < array.length; i++) {
    var counter = 0;
    for(var j = i; j < array.length; j++) {
      if(array[i] === array[j]) {
        counter++;
      }
    }
    if(counter > highest) {
      var mode = array[i];
      highest = counter;
    }
  }

  return mode;
};

// example input: [1, 2, 3, 4, 4, 2, 1, 1]
// mode: 1

{% endhighlight %}

The time complexity of this algorithm is O(n^2) because the time it takes to solve the problem
increases by the length of the array squared. This means the algorithm is scaling very
poorly with large data sets to a point where it might not even be useful.

**Taking advantage of objects**

A better approach to finding the mode is to count up repeated numbers within an object. With all
this information saved, the nested loop becomes unnecessary.

{% highlight javascript %}

var storageMode = function(array) {
  var storage = {};
  var highest = 0;

  for(var i = 0; i < array.length; i++) {
    var key = array[i];
    if(storage[key] === undefined) {  // check if the key doesn't exist
      storage[key] = 1;  // create key and set the initial value to 1
    } else {
      storage[key]++;  // add 1 if the key already exists
    }
    if(storage[key] > highest) {
      var mode = key;
      highest = storage[key];
    }
  }

  return mode;
};

// example input: [2, 2, 3, 4, 4, 2, 1, 1]
// storage will look like: {'1': 2, '2': 3, '3': 1, '4': 2}
// mode: 2

{% endhighlight %}

Here we can see that the object in this algorithm requires more space in memory, 
but the removal of the nested for loop means this algorithm has O(n) time complexity because it scales
linearly as the size of the array increases.

To put this into perspective, if an array of size 100 is passed into the first algorithm, the
time it takes to complete will increase by an order of 10000, yet the second algorithm
will only increase by an order of 100. This is a very noticeable difference with large arrays.

**Trading space for speed**

Optimization is often about tradeoffs; improving one aspect of your code may require a sacrifice
elsewhere. When using objects to store data, the goal is to increase the speed of the algorithm
at a cost to storage. In most cases, this is a very good trade because processing power is much
more valuable than memory.