---
layout: post
title:  "LongestSubstringWithoutRepeatingCharacters"
date:   2016-09-07 20:30:00 +0800
categories: arithmetic
---


Q:
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

----------

A:给定一个字符串，求最长的字符不重复的子字符串。

这道题的第一直觉是确定左侧锚点，向右便利，用map来记录出现过的字符，如果遇到重复字符，则记录此前的子字符串，和当前最长的子字符串作比较；之后把左侧锚点右移一位，继续这个流程，直到左侧锚点走完整个字符串长度。代码如下


{% highlight c++ %}

	//c++ version
	
	#include <iostream>
	#include <string>
	#include <map>
	
	
	using namespace std;
	
	string longestSubstringWithoutRepeatingCharacters(string str) {
	    string result;
	    
	    
	    unsigned long length = str.length();
	    for (int i = 0; i < length; i++) {
	        int j = i;
	        
	        string tmp;
	        map<char, bool> hit;
	        
	        while (j < length) {
	            char cur = str[j];
	            if (hit.find(cur) != hit.end()) {
	                break;
	            } else {
	                tmp += cur;
	                hit.insert(pair<char, bool>(cur, true));
	            }
	            j++;
	        }
	        
	        result = tmp.length() > result.length() ? tmp : result;
	    }
	    
	    return result;
	}

{% endhighlight %}



这一基础方案的时间复杂度是O(n)，仔细想了，有个点我们可以做优化：

当发现重复字符时，左侧可以直接移到重复字符后一位，以减少遍历的次数。

比如说，qewabcabcbb 这个字符串，第一次遍历，左侧为第0位，右侧首次遇到重复字符是第6位的 **a** ， 重复的是第3位的 **a**。按照基础方案，此时我们把左侧移到第1位，继续第二次遍历，会发现右侧遇到的重复情况还是一样的，也就是说，只要右侧包含第3位的 **a**，就会发生和第一次相同的重复。我们可以把左侧直接移到第3位的后一位，再开始遍历，以减少遍历次数。

在这一优化方案中，map的key还是字符串中的字符，value改为该字符在字符串中的索引。左侧移到被重复字符后，要把map中这个字符的value修改为重复字符的索引（在qewabcabcbb这个例子里， 把map 中 **a** 的value，修改为6）

优化后的方案如下：


{% highlight c++ %}

	string longestSubstringWithoutRepeatingCharacters2(string original) {
	    string result;
	    
	    unsigned long length = original.length();
	    int i = 0, j = 0;
	    map<char, int> hit; //key is element, value is index
	    string tmp;
	    
	    while (i < length && j < length) {
	        char cur = original[j];
	        if (hit.find(cur) != hit.end()) { //hit
	            result = tmp.length() > result.length() ? tmp : result;
	            i = hit[cur] + 1;
	            tmp = original.substr(i, j-i+1);
	            hit[cur] = j;
	            j++;
	            
	        } else { //miss
	            hit[cur] = j;
	            tmp += cur;
	            j++;
	        }
	    }
	    
	//    if not hit at all
	    if (result == "") {
	        result = tmp;
	        
	    }
	    
	    return result;
	}

{% endhighlight %}

Check out the [C++ Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/LongestSubstringWithoutRepeatingCharacters