---
layout:     post
title:      "Letter Combinations of a Phone Number"
subtitle:   "Leetcode-17"
date:       2017-10-17 23:46:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Letter Combinations of a Phone Number
## Question

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![](post.png)
```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
## Answer
一类回溯问题，递归调用可求解
```py
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        res = []
        if digits == "":
            return res
        my_dict = {2:['a', 'b', 'c'], 3:['d', 'e', 'f'], 4:['g', 'h', 'i'], 
                   5:['j', 'k', 'l'], 6:['m', 'n', 'o'], 7:['p', 'q', 'r', 's'], 
                   8:['t', 'u', 'v'], 9:['w', 'x', 'y', 'z']}
        for i in range(len(digits)):
            if i == 0:
                res = my_dict[int(digits[i])]
            else:
                res = [x + y for x in res for y in my_dict[int(digits[i])]]
        return res     
```