---
layout: post
title:  "Add Binary"
date:   2016-08-05 12:30:00 +0800
categories: arithmetic
---
开始刷点算法题，代码用swift

Q:
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

----------

A:
二进制数的求和。这题涉及到字符串操作，用swift实在太难弄了（swift的String, characters, index简直呵呵），所以swift版本先转成数字然后做加法。纯字符操作用c++写起来就舒服多了

{% highlight swift %}

// swift version
extension String {
    subscript (i: Int) -> String {
        return String(self[self.endIndex.advancedBy(-1-i)])
    }
}

func addBinary(a: String, _ b: String) -> String {
    let n_a = Int(a)!
    let n_b = Int(b)!
    
    var sum = n_a + n_b
    let target = 2
    
    var i = 0
    var next = 0
    var res = String()
    
    while sum / 10 > 0 || sum > 0 {
        let digit = sum % 10
        let cur: String = String(digit % target)
        res.insert(cur[cur.startIndex], atIndex: res.startIndex)
        next = digit / target
        
        sum = sum / 10 + next
        i = i + 1
    }
    
    return String(res)
}

{% endhighlight %}

Check out the [Codes][codes].

[codes]: https://github.com/JingWZ/ArithmeticSorting/tree/master/AddBinary.playground

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

Check out the [Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/AddBinaryCPP