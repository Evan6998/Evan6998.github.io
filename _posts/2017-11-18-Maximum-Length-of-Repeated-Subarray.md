---
layout:     post
title:      "Maximum Length of Repeated Subarray"
subtitle:   "Leetcode-718"
date:       2017-11-18 19:04:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Maximum Length of Repeated Subarray
## Question
Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.

**Example 1:**
```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```
**Note:**
1. 1 <= len(A), len(B) <= 1000
2. 0 <= A[i], B[i] < 100

## Answer
这道题应该是属于最长公共子序列类型的题目，并且要求连续。
刚开始暴力解，直接双循环里加while结果Runtime Error.  
```py
class Solution(object):
    def findLength(self, A, B):
        """
        :type A: List[int]
        :type B: List[int]
        :rtype: int
        """
        maxLen = 0
        for i in range(len(A)):
            for j in range(len(B)):
                if A[i] == B[j]:
                    m, n = i, j
                    curLen = 0
                    while m != len(A) and n != len(B) and A[m] == B[n]:
                        m += 1
                        n += 1
                        curLen += 1
                    maxLen = curLen if curLen > maxLen else maxLen
        return maxLen
```
然后开始考虑动态规划。前一种算法的问题在于每个(i, j)内的公共子序列长度都得重新算，所以计算量较大。因此我们维护一个矩阵来保存(i, j)的公共子序列长度。  
这个矩阵第i行第j列的数值代表到数组A的第i个元素和B的第j个元素为止时的最长公共子序列长度。
```PY
class Solution(object):
    def findLength(self, A, B):
        """
        :type A: List[int]
        :type B: List[int]
        :rtype: int
        """
        maxLen = 0
        dp = [[0 for i in range(len(A)+1)] for j in range(len(B)+1)]
        for i in range(1, len(A)+1):
            for j in range(1, len(B)+1):
                if A[i-1] == B[j-1]:
                    dp[i][j] = dp[i-1][j-1]+1
        return max([max(row) for row in dp])
```