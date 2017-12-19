---
layout:     post
title:      "Delete and Earn"
subtitle:   "Leetcode-740"
date:       2017-12-19 10:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Delete and Earn
## Question

Given an array `nums` of integers, you can perform operations on the array.

In each operation, you pick any `nums[i]` and delete it to earn `nums[i]` points. After, you must delete every element equal to `nums[i] - 1` or `nums[i] + 1`.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.

### Example 1
```
Input: nums = [3, 4, 2]
Output: 6
Explanation: 
Delete 4 to earn 4 points, consequently 3 is also deleted.
Then, delete 2 to earn 2 points. 6 total points are earned.
```

### Example 2
```
Input: nums = [2, 2, 3, 3, 3, 4]
Output: 9
Explanation: 
Delete 3 to earn 3 points, deleting both 2's and the 4.
Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
9 total points are earned.
```

### Note:
- The length of `nums` is at most `20000`.
- Each element `nums[i]` is an integer in the range `[1, 10000]`.

## Answer
这个问题有两个点：  
1. 解与问题的输入数组顺序无关。
2. 这是一个动态规划问题。

我们可以通过将每一种数字的值累加起来，得到每一种数字的总和。比如：  
[2, 2, 3, 3, 3, 4] -> [0, 0, 4, 9, 4]即将对应的0,1,2,3,4的数字的和加起来赋值到对应的下标。  

代码如下
```py
class Solution(object):
    def deleteAndEarn(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numSum = [0]*10001
        dp = [0] * 10001
        for num in nums:
            numSum[num] += num
        for i in range(1, len(dp)):
            if i == 1: dp[i] = numSum[i]
            else: dp[i] = max(dp[i-1], dp[i-2]+numSum[i])
        return max(dp)
``` 