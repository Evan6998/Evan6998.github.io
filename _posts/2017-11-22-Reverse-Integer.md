---
layout:     post
title:      "Reverse Integer"
subtitle:   "Leetcode-7"
date:       2017-11-22 00:40:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Reverse Integer
## Question

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**
```
Input: 123
Output:  321
```
**Example 2:**
```
Input: -123
Output: -321
```
**Example 3:**
```
Input: 120
Output: 21
```
**Note:**
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Answer
问题不算难，设置一个while然后求余并除应该可以得到结果
```c++
class Solution {
public:
    int reverse(int x) {
        int temp = x;
        int result = 0;
        while(temp) {
            result = result*10 + temp % 10;
            temp /= 10;
        }
        return result;
    }
};
```

但是题目有一个要求：机器是运行在32位的系统上的，溢出时需要改为0。   
因此需要修改。

首先我们将结果改为long long的类型，再去判断结果是否超过32位的最值
```cpp
long long result = 0;
...
return (result > INT_MAX || result < INT_MIN) ? 0 : result;
```


