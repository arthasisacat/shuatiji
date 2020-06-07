---
title: 44. Minimum Subarray
parent: DP
has_children: false
weight: 5
permalink: lintcode44
---
# 44. Minimum Subarray
[lintcode link](https://www.lintcode.com/problem/minimum-subarray/description)

**difficulty(1-5)** 
2

**notes**   
Didn't find same problem in leetcode 

## Description
Given an array of integers, find the subarray with smallest sum.
Return the sum of the subarray.
The subarray should contain one integer at least.Have you met this question in a real interview?  YesProblem Correction
Example
For [1, -1, -2, 1], return -3.

## Solution
没什么好说的, 和 maximum subarray 一样.
i 从 0~n-1 遍历, 每次循环中 可能的最小subarray sum 就是 sum - history_max. 打擂台

```c++
class Solution {
public:
    /*
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
    int minSubArray(vector<int> &nums) {
        if (nums.size() == 0) {
            return 0;
        }
        int sum = nums[0];
        int max_val = max(0, nums[0]);
        int res = nums[0];
        for (int i = 1; i < nums.size(); i ++) {
            sum += nums[i];
            res = min(res, sum - max_val);
            max_val = max(max_val, sum);
        }
        return res;
    }
};
```