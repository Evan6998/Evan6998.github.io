---
layout:     post
title:      "Search a 2D Matrix II"
subtitle:   "Leetcode-240"
date:       2017-09-17 10:55:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---

# Search a 2D Matrix II
## Question
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.  

For example,

Consider the following matrix:
```py
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given **target** = 5, return `true`.

Given **target** = 20, return `false`.

## Answer
刚开始我就简单地去遍历这个matrix并设置了一些限制条件，结果发现Runtime倒数了。排位为`2.24%`(倒数)  
代码如下
```PY
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] == target:
                    return True
                elif matrix[i][j] > target:
                    break
            if matrix[i] and matrix[i][0] > target:
                return False
        return False
```
然后就试着用了二分法来找。排位为`21.28%`左右，代码如下：
```py
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        def bs(nums, target):
            l, r = 0, len(nums) - 1
            while l <= r:
                mid = (l + r) / 2
                if nums[mid] == target: return True
                elif nums[mid] > target: r = mid - 1
                else: l = mid + 1
            return False
        
        for i in range(len(matrix)):
            if matrix[i] and matrix[i][0] > target: return False
            if matrix[i]:
                if bs(matrix[i], target): return True
        return False
```