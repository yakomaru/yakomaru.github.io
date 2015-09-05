---
title:  "testing go code"
date:   2015-09-05 13:30:00
categories: go, testing
---

A quick overview of how to write tests for the Go programming language.


**Test Driven Development**

When writing code, it's important to keep things modular so that the code is easier to read, reuse, and test. In Go, this remains true as small modular functions are much easier to test and possibly fix than large chunks of code.

**How to Setup a Go Test**

Go has a built in testing framework that makes testing code easy and manageable. To start testing Go code, simply make a `.go` file and give it the same name as the desired file to be tested, but with a `_test` after it (eg: `main_test.go`). The test can easily be run with the `go test` command on the folder containing the code being tested and the test file itself. Optionally, the `-v` tag can be thrown in to see the outcome of each test (eg: `go test .\main -v`).

**Example Go Test File**

Here is a quick overview with comments explaining what each section is for:

{% highlight go %}

package main_test

import (
  // the Go testing package
  "testing"

  // the code being tested
  "github.com/user/project/main"
)

var (
  // globals used in multiple tests can go here
)

func init() {
  // put anything here that needs to run before the tests
}

// note that the function starts with 'Test'
func TestOne(t *testing.T) {
  // run code as needed from the package being tested
  sum, err := main.Sum(1, 1)

  if err != nil {
    // test.Error() is used if something goes wrong
    t.Error(err)
  }

  // when the output is wrong, this error is fired
  if sum != 2 {
    t.Errorf("Expected:", sum, "to be", 2)
  }
}

func TestTwo(t *testing.T) {
  // more tests
}

{% endhighlight %}

The Go testing framework is farily straight forward and easy to use so long as the code being tested is written with the testing framework in mind and is kept modular with testable inputs and outputs.
