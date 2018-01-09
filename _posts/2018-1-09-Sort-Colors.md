---
layout:     post
title:      "Sort Colors"
subtitle:   "Leetcode-75"
date:       2017-01-09 23:46:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Sort Colors
## Question
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

**Note:**
You are not suppose to use the library's sort function for this problem.

## Answer
因为是一道基数排序的题，所以也放上来。  
首先，这种数据范围比较小的可以直接用基数排序来做，用空间换时间。代码入下。
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        vector<int> temp(3,0);
        for (auto i : nums) {
            temp[i]++;
        }
        int index = 0;
        for (auto i = 0; i < temp.size(); i++) {
            while(temp[i]--) {
                nums[index++] = i;
            } 
        }
    }
};
```

建立三个桶，分别用来放0，1，2这三种颜色，排序过程中每遇到一种颜色就往改值+1，最后复原时直接拷贝各种颜色的数量上去即可。