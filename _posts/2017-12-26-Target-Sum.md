---
layout:     post
title:      "Target Sum"
subtitle:   "Leetcode-494"
date:       2017-12-26 10:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Target Sum
## Question
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols `+` and `-`. For each integer, you should choose one from `+` and `-` as its new symbol.  

Find out how many ways to assign symbols to make sum of integers equal to target S.
**Example 1:**
```
Input: nums is [1, 1, 1, 1, 1], S is 3. 
Output: 5
Explanation: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
```
**Note:**
1. The length of the given array is positive and will not exceed 20.  
2. The sum of elements in the given array will not exceed 1000.  
3. Your output answer is guaranteed to be fitted in a 32-bit integer.  

## Answer
这道题刚开始看到时是想着用动态规划来做，但是没想出转移方程，就打算用递归来做，把所有的都列一遍。代码：
```py
class Solution(object):
    count = 0
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        length = len(nums)
        def helper(currsum, pos):
            if pos == length:
                if currsum == S: self.count+=1
            else:
                helper(currsum+nums[pos], pos+1)
                helper(currsum-nums[pos], pos+1)
        helper(0, 0)
        return self.count
```
But unfortunately,超时了，所以决定做个记忆化，保存下计算过的值。
```py
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        length = len(nums)
        import sys
        dp = [[-sys.maxint]*2001 for i in range(length)]
        def helper(currsum, pos):
            if pos == length:
                return 1 if currsum == S else 0
            else:
                if dp[pos][currsum+1000] != -sys.maxint:
                    return dp[pos][currsum+1000]
                add = helper(currsum+nums[pos], pos+1)
                sub = helper(currsum-nums[pos], pos+1)
                dp[pos][currsum+1000] = add + sub
                return dp[pos][currsum+1000]
        return helper(0, 0)
```

Solved.