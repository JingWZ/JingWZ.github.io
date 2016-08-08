---
layout: post
title:  "Add Binary"
date:   2016-08-05 12:30:00 +0800
categories: arithmetic
---


Q:
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

----------

A:
二进制数的求和。这题涉及到字符串操作，~~用swift实在太难弄了（swift的String, characters, index简直呵呵），所以swift版本先转成数字然后做加法~~。纯字符操作用c++写起来就舒服多了

更新：仔细想了下还是不应该转数字然后做加法，删除swift版本的方案。如果相加的两个数位数很大，可能存不进int中，性能也不好；另外如果两个数位数相差多，也不合适转。相反直接取字符串操作灵活很多


{% highlight c++ %}

//c++ version
string addBinary(string a, string b) {
    int i = (int)a.length();
    int j = (int)b.length();
    int cur = 0;
    string res;
    
    while (i || j || cur) {
        cur += (i ? a[(i--)-1] - '0' : 0) + (j ? b[(j--)-1] - '0' : 0);
        res = char(cur%2 + '0') + res;
        cur /= 2;
    }
    
    return res;
}

{% endhighlight %}

Check out the [C++ Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/AddBinaryCPP