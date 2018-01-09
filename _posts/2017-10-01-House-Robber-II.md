---
layout:     post
title:      "House Robber II"
subtitle:   "Leetcode-213"
date:       2017-10-01 10:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# House Robber II
## Question
**Note**: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police.**

## Answer
House Robber的变种，解决方法还是动态规划，不过需要变一下。我们将这个园割开，分别取不要起点或者不要终点的部分来做。然后返回最大的。
```py
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        def subRob(subNums):
            if not subNums: return 0
            dp = [0] * len(subNums)
            for i in range(len(subNums)):
                if i == 0: dp[i] = subNums[i]
                elif i == 1: dp[i] = max(subNums[:2])
                else: dp[i] = max(dp[i-1], dp[i-2]+subNums[i])
            return dp[-1]
        if len(nums) == 1: return nums[0]
        return max(subRob(nums[1:]), subRob(nums[:-1]))
```