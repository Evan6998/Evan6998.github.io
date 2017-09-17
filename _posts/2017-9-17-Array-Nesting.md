---
layout:     post
title:      "Array Nesting"
subtitle:   "Leetcode-565"
date:       2017-09-17 10:55:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---

# Array Nesting
## Question
A zero-indexed array A consisting of N different integers is given. The array contains all integers in the range [0, N - 1].

Sets S[K] for 0 <= K < N are defined as follows:

S[K] = { A[K], A[A[K]], A[A[A[K]]], ... }.

Sets S[K] are finite for each K and should NOT contain duplicates.

Write a function that given an array A consisting of N integers, return the size of the largest set S[K] for this array.

**Example 1:**
```
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation: 
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```
**Note:**
1. N is an integer within the range [1, 20,000].  
2. The elements of A are all distinct.  
3. Each element of array A is an integer within the range [0, N-1].  

## Answer
### Answer1
这道题看到时就打算
- 保存一个marked数组用来标记已经访问过的元素
- count和maxC用来记录最大的nestArray  

然后遍历一遍，每次将访问过的mark一下，代码如下
```py
class Solution(object):
    def arrayNesting(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        marked = [0] * len(nums)
        count, maxC = 0, 0
        for i in range(len(nums)):
            ii = i
            while not marked[ii]:
                marked[ii] = 1
                ii = nums[ii]
                count += 1
            maxC = max(count, maxC)
            count = 0
        return maxC
```

### Answer2
不过在discussion看到别人的解法如下
```C++
class Solution {
public:
    int arrayNesting(vector<int>& a) {
        size_t maxsize = 0;
        for (int i = 0; i < a.size(); i++) {
            size_t size = 0;
            for (int k = i; a[k] >= 0; size++) {
                int ak = a[k];
                a[k] = -1; // mark a[k] as visited;
                k = ak;
            }
            maxsize = max(maxsize, size);
        }

        return maxsize;
    }
};
```
仔细想一下就可以发现其实没有必要保存一个marked的数组，因为不同的nestArray实际上并不会相交，遍历的过程只需要将原数组给marked就ok了