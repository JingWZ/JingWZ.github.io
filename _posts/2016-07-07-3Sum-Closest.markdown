---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-07-04 19:53:51 +0800
categories: jekyll update
---
开始刷点算法题，代码用swift

Q:
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

For example, given array S = {-1 2 1 -4}, and target = 1.
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).


A:
数组l[n]，求3个元素的和最接近某个给定值t。思路是逼近，排序后两个循环求值，复杂度O(n^2)。假设元素是i,j,k, 固定i, j=i+1，k=n-1，j向右逼近，k向左逼近，直到找出最接近的值。

{% highlight swift %}
func compute3SumClosest(list:[Int], _ target:Int) -> Int {
    if list.count <= 3 {
        return list.reduce(0, combine: {$0+$1})
    }
    
    var sorted = list.sort()
    var res = sorted[0] + sorted[1] + sorted[2]
    
    for i in 0..<sorted.count - 2 {
        var j = i + 1
        var k = sorted.count - 1
        while j < k {
            let sum = sorted[i] + sorted[j] + sorted[k]
            if abs(sum - target) < abs(res - target) {
                res = sum
                if res == target {
                    return res
                }
            }
            
            sum > target ? k-- : j++
        }
    }
    
    return res
}
{% endhighlight %}

Check out the [Codes].

[codes]: http://jekyllrb.com/docs/home
