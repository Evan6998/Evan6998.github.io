---
layout:     post
title:      "Predict the Winner"
subtitle:   "Leetcode-486"
date:       2017-11-02 20:12:00
author:     "Evan"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Algorithms
---
# Predict the Winner
## Question
Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.
**Example 1**
```
Input: [1, 5, 2]
Output: False
Explanation: Initially, player 1 can choose between 1 and 2. 
If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. 
Hence, player 1 will never be the winner and you need to return False.
```
**Example 2**
```
Input: [1, 5, 233, 7]
Output: True
Explanation: Player 1 first chooses 1. Then player 2 have to choose between 5 and 7. No matter which number player 2 choose, player 1 can choose 233.
Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.
```
**Note**
1. 1 <= length of the array <= 20.  
2. Any scores in the given array are non-negative integers and will not exceed 10,000,000.  
3. If the scores of both players are equal, then player 1 is still the winner.  

## Answer
这道题很有意思，也是书本课后的原题。这是一道动态规划求解的题目，主要的难点在于转移方程很难看出来。  
首先这道题是默认了前后双方都是能取到当前的最大利益，也就是我们的算法对两个人（转移方程）都是适用的。  
那么，我们定义dp[i][j]为在这个数组的第i个数到第j个数之间，第一个人能取到的最大值。注意，这个值代表了在双方都是最佳选择，也就是说，这个值有两种结果，一是为正，代表在i，j范围内第一个人赢了；或者结果为负，代表第一个人输了。结果就代表在i，j内赢了或输了多少。  
那么对于某个人在当前的状态，dp[i][j]是他的结果。他只有两种选择，一是拿最左，而是拿最右。  
即，当拿最左时，剩下的dp[i+1,j]就是另一个人的结果。   
这两个结果的关系应该是：dp[i][j] = v[i]-dp[i+1][j]。比如最左的值为10，然后剩下最好的结果dp[i+1,j]的值为5，那最终结果为10-5=5，第一个人胜。  
若dp[i+1][j] = 15, 则dp[i][j] = 10-15=-5,第一个人输。
```c++
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        if (nums.size() < 3) return true;
        auto dp = vector<vector<int>>(nums.size()+1, vector<int>(nums.size()+1, 0));
        for (auto i = 1; i < nums.size()+1; i++) dp[i][i] = nums[i-1];
        for (auto i = 1; i < nums.size()+1; i++) {
            for (auto j = 1; j+i < nums.size()+1; j++) {
                int r = i+j;
                dp[j][r] = max(nums[j-1]-dp[j+1][r], nums[r-1]-dp[j][r-1]);
            }
        }
        return dp[1][nums.size()-1] >= 0;
    }
};
```