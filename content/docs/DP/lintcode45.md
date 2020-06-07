---
title: 45. Maximum Subarray Difference
parent: DP
has_children: false
weight: 5
permalink: /docs/lintcode45 
---
# 45. Maximum Subarray Difference
[lintcode link](https://www.lintcode.com/problem/maximum-subarray-difference/description?_from=ladder&&fromId=1)

**difficulty(1-5)** 
4

**notes**   
看着很简单,实则很难写对.... T.T

## Description
Given an array with integers.
Find two non-overlapping subarrays A and B, which |SUM(A) - SUM(B)| is the largest.
Return the largest difference.
**The subarray should contain at least one number**
Example
For [1, 2, -3, 1], return 6.
**
Challenge
O(n) time and O(n) space.**


## Solution

简单来说就是从左往右算 min subarray 和 max subarray, 然后从右往左算一样的东西. 
但是由于要求左右两边的 subarray 都不是空的,所以以往 prefix sum 的算法(从前0个开始算) 是不适用的.

**需要从第一个元素开始算min/max, 而不是第零个!**

```c++
class Solution {
public:
    void print_arr(vector<int>& arr) {
        for (auto n : arr) {
            cout<<n<<" ";
        }
        cout<<endl;
    }
    /**
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two substrings
     */
    int maxDiffSubArrays(vector<int> &nums) {
        int n = nums.size();
        
        vector<int> max_l(n), max_r(n), min_l(n), min_r(n);
        int sum = 0;
        int min_sum = 0;
        int max_sum = 0;
        int cur_max = INT_MIN;
        int cur_min = INT_MAX;
        for (int i = 0; i < n; i++) {
            sum += nums[i];
            cur_max = max_l[i] = max(cur_max, sum - min_sum);
            cur_min = min_l[i] = min(cur_min, sum - max_sum);
            min_sum = min(min_sum, sum);
            max_sum = max(max_sum, sum);
        }
        
        sum = 0;
        min_sum = 0; 
        max_sum = 0;
        cur_max = INT_MIN;
        cur_min = INT_MAX;
        for (int i = n-1; i >= 0; i--) {
            sum += nums[i];
            cur_max = max_r[i] = max(cur_max, sum - min_sum);
            cur_min = min_r[i] = min(cur_min, sum - max_sum);
            min_sum = min(min_sum, sum);
            max_sum = max(max_sum, sum);
        }
        
        // print_arr(max_l);
        // print_arr(min_l);
        // print_arr(max_r);
        // print_arr(min_r);
        
        int res = INT_MIN;
        for (int i = 0; i < n-1; i++) {
            int tmp = max(abs(max_l[i] - min_r[i+1]), abs(min_l[i] - max_r[i+1]));
            res = max(res, tmp);
        }
        return res;
    }
};
```