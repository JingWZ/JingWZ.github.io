---
layout: post
title:  "Group Anagrams"
date:   2016-09-05 20:30:00 +0800
categories: arithmetic
---


Q:
Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"],
Return:

[
 ["ate", "eat","tea"],
 ["nat","tan"],
 ["bat"]
 ]
Note: All inputs will be in lower-case.

----------

A:
给定一个字符串数组，把数组中，字符串组成一致的分组并返回。


{% highlight c++ %}

#include <iostream>
#include <string>
#include <algorithm>
#include <map>
#include <vector>

using namespace std;

//c++ version

void GroupAnagrams() {
    vector<string> a = {"eat", "tea", "tan", "ate", "nat", "bat"};
    map<string, vector<string>> dict;
    map<string, vector<string>>::iterator iter;
    
    for (int i = 0; i < 6; i++) {
        string str = a[i];
        string original = str;
        sort(str.begin(), str.end());
        
        iter = dict.find(str);
        vector<string> col;
        if (iter != dict.end()) {
            col = dict[str];
        }
        
        col.push_back(original);
        dict[str] = col;

    }
    
    vector<vector<string>> res;
    for (map<string, vector<string>>::iterator iter = dict.begin(); iter != dict.end(); ++iter) {
        vector<string> col = iter->second;
        res.push_back(col);
        
        //结果输出 for debug
//        for (vector<string>::iterator it = col.begin(); it != col.end(); ++it) {
//            cout << *it << ",";
//        }
//        cout << "\n";
    }
}

{% endhighlight %}

Check out the [C++ Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/GroupAnagramsCPP