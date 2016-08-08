---
layout: post
title:  "Add Two Numbers"
date:   2016-08-08 12:30:00 +0800
categories: arithmetic
---


Q:
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
 
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

----------

A:
链表操作，求和。一开始没理解题目意思，以为是要反向位数相加再进位，直接跪倒。后来看答案才知道是自己想复杂了，直接正向相加进位就可以。要注意两个链表不同个数和进位。涉及到指针，还是用c++


{% highlight c++ %}

//c++ version

//结构体，既可以表示链表的单个节点，又可以表示链表本身（第一个节点即表明链表本身）
typedef struct LinkedNode
{
    int data;
    LinkedNode *next;
    
}LinkedNode;

//生成链表方法
LinkedNode* LinkedNodeMake(int n, ...) {
    
    va_list args;
    va_start(args, n);
    
    LinkedNode *prev = new LinkedNode;
    prev->data = va_arg(args, int);
    LinkedNode *head = prev;
    
    for (int i = 1; i < n; i++) {
        LinkedNode *node = new LinkedNode;
        node->data = va_arg(args, int);
        prev->next = node;
        
        prev = node;
    }
    va_end(args);
    
    return head;
}

//Add Two Numbers函数
LinkedNode* AddTwoNumbers(LinkedNode* a, LinkedNode* b) {
    int cur = 0;
    LinkedNode preHead = {};
    LinkedNode *node = &preHead;
    
    while (a || b || cur) {
        int sum = (a ? a->data : 0) + (b ? b->data : 0) + cur;
        LinkedNode *tmp = new LinkedNode;
        tmp->data = sum%10;
        
        node->next = tmp;
        node = tmp;
        
        cur = sum/10;
        a = a ? a->next : NULL;
        b = b ? b->next : NULL;
    }
    return preHead.next;
}

//如何使用
int main(int argc, const char * argv[]) {
    // insert code here...
    
    
    LinkedNode *a = LinkedNodeMake(3, 2,4,3);
    LinkedNode *b = LinkedNodeMake(3, 5,6,4);
    LinkedNode *sum = AddTwoNumbers(a, b);
    
    while (sum) {
        std::cout << sum->data;
        std::cout << ",";
        sum = sum->next;
    }
    
    std::cout << "\n";
    return 0;
}

{% endhighlight %}

Check out the [C++ Codes][codes1].

[codes1]: https://github.com/JingWZ/ArithmeticSorting/tree/master/AddTwoNumbersCPP