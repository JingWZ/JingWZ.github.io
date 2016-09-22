---
layout: post
title:  "Reverse Integer"
date:   2016-09-21 20:30:00 +0800
categories: arithmetic
---


Q:

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

----------

A:

{% highlight swift %}

	//swift version

	func reverseInteger(original:Int) -> Int {
	    var result = 0
	    
	    var numbs = original
	    while numbs != 0 {
	        result = result * 10 + numbs % 10
	        numbs = numbs / 10
	    }
	    
	    return result
	}


{% endhighlight %}


Check out the [swift Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/ReverseInteger.playground