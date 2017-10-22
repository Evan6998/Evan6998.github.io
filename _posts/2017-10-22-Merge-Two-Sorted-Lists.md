---
layout:     post
title:      "Merge Two Sorted Lists"
subtitle:   "Leetcode-21"
date:       2017-10-22 19:04:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---

# Merge Two Sorted Lists
## Question
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Answer
这道题比较简单，就是归并的链表版本。在归并时可以利用链表的特性结合归并来完成。

对于两个链表，当其中某一条为NULL时，直接返回另一条即可。  
其他情况，比较两个链表的首元素，选择较大的那一条，然后递归调用这一条的下一个节点开始的链表和另一条链表的归并。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1) return l2;
        if(!l2) return l1;
        
        if(l1 -> val < l2 -> val) {
            l1 -> next = mergeTwoLists(l1 -> next, l2);
            return l1;
        } else {
            l2 -> next = mergeTwoLists(l2 -> next, l1);
            return l2;
        }
    }
};
```