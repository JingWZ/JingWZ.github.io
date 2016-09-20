---
layout: post
title:  "ZigZag Conversion"
date:   2016-09-20 20:30:00 +0800
categories: arithmetic
---


Q:
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
 
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:

string convert(string text, int nRows);
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

----------

A:字符串排列题目，一开始看的时候没理解到底是怎么排的，后来去搜了下才明白，是把一串字符，纵向按照倒N形状排列，然后再横向输出结果。

举例来说，一个字符串abcdefghijklmnopqrst，排成5行，就是


	a       i       q
	b     h j     p r 
	c   g   k   o   s
	d f     l n     t
	e       m

可以发现，在第1行和第5行，同一行的两个字符在元字符串中相隔（n + n - 2）位字符，而在其他行数，相隔的位数取决于行数。根据这个规律，针对行数做循环，每一行从元字符串中抽取相应位数的字符拼起来，最终得到的就是答案。

{% highlight c++ %}

	//c++ version

	string convert(string text, int nRows) {
	    if (nRows <= 1) {
	        return text;
	    }
	    
	    string res;
	    unsigned long length = text.length();
	    int round = nRows + nRows - 2;
	    
	    for (int i = 0; i < nRows; i++) {
	        int j = i;
	        int det = round - j * 2;
	        while (j < length) {
	            res.append(text, j, 1);
	            if (det != round && det != 0 && j + det < length) {
	                res.append(text, j + det, 1);
	            } else if (j + det >= length) {
	                break;
	            }
	            j += round;
	        }
	    }
	    
	    return res;
	}

{% endhighlight %}


Check out the [C++ Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/ZigZag_Conversion