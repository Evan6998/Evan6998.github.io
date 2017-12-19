---
layout:     post
title:      "Palindromic Substrings"
subtitle:   "Leetcode-647"
date:       2017-10-10 10:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Palindromic Substrings
## Question
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
**Example 2:**
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```
**Note:**
The input string length won't exceed 1000.

## Answer
这道题是一道比较常见的动态规划，状态转移方程为：  
dp[i][j] = dp[i+i][j-1]  
其中，i，j分别表示下标i到下标j是否为回文串。代码如下：
```py
class Solution(object):
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        dp = [[1 if j >= i else 0 for i in range(len(s))] for j in range(len(s))]
        for i in range(1, len(s)):
            for j in range(len(s)-i):
                if s[j] == s[j+i]: dp[j][j+i] = dp[j+1][j+i-1]  
        count = 0
        for i in range(len(dp)):
            for j in range(len(dp)):
                if j >= i and dp[i][j] == 1: count +=1
                    
        return count
```