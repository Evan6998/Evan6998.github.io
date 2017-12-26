---
layout:     post
title:      "Unique Paths"
subtitle:   "Leetcode-62"
date:       2017-12-18 10:55:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Unique Paths
## Question
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).  

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).  

How many possible unique paths are there?  
## Answer
这个网格中每一步都可以从上面或者左边走到，所以当前格子的数目等于上面的数值加上左边的数值。
```py
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        a = [[1 for i in range(n)] for i in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                a[i][j] = a[i-1][j] + a[i][j-1]
        return a[m-1][n-1]
```