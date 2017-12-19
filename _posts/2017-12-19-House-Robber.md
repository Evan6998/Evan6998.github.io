---
layout:     post
title:      "House Robber"
subtitle:   "Leetcode-198"
date:       2017-12-14 10:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# House Robber
## Question
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police.**
## Answer
简单的动态规划问题，状态转移方程为：`dp[i] = max(dp[i-1], dp[i-2]+nums[i])`

```py
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        dp = [0]*len(nums)
        for i in range(len(dp)):
            if i == 0: dp[i] = nums[0]
            elif i == 1: dp[i] = max(nums[:i+1])
            else: dp[i] = max(dp[i-1], dp[i-2]+nums[i])
        return dp[-1]
```
