---
layout:     post
title:      "Leetcode-46 Permutations"
subtitle:   "Blog for Leetcode"
date:       2017-09-10 11:12:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---

# Permutations
## Question
Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
```py
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
## Solution
这是一道典型的回溯题，通过不断递归即可找到所有解
```py
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        ret = []
        def back(nums, p = []):
            if not nums:
                ret.append(p)
                return
            for i in range(len(nums)) :
                back(nums[:i] + nums[i+1:], p + [nums[i]])
        back(nums)
        return ret
```