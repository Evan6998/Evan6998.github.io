---
layout:     post
title:      "Kth Largest Element in an Array"
subtitle:   "Leetcode-215"
date:       2017-09-15 19:24:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---

# Kth Largest Element in an Array
## Question
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
Given `[3,2,1,5,6,4]` and k = 2, return 5.

**Note:**   
You may assume k is always valid, 1 ≤ k ≤ array's length.

## Answer
`类型：归并排序`  
这道题类似与快速排序的算法，为了能在O(n)的时间复杂度内完成，先使用`partition`来进行切分，能够返回一个数组中某个数的大小排位，同时该数左边的数比它小，右边的数比他大。因此通过这种递归可以找到第k大的数。
```py
class Solution(object):
    def partition(self, nums, low, high):
        l, r = low, high
        c = nums[r]
        while(l < r):
            while(nums[l] < c and l < r): l += 1
            while(nums[r] >= c and l < r): r -= 1
            nums[l], nums[r] = nums[r], nums[l]
        nums[r], nums[high] = nums[high], nums[r]
        return r
    
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        from random import shuffle
        shuffle(nums)
        l, h = 0, len(nums) - 1
        k = len(nums) - k
        while(h > l):
            j = self.partition(nums, l, h)
            if j == k: return nums[k]
            elif j > k: h = j - 1
            elif j < k: l = j + 1
        return nums[k]
```