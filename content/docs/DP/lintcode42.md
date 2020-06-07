---
title: 42. Maximum Subarray II
parent: DP
has_children: false
weight: 5
permalink: lintcode42
---
# 42. Maximum Subarray II
[lintcode link](https://www.lintcode.com/problem/maximum-subarray-ii/description?_from=ladder&&fromId=1)

**difficulty(1-5)** 
3

**notes**   
Didn't find same problem in leetcode 

## Description
Given an array of integers, find two non-overlapping subarrays which have the largest sum.
The number in each subarray should be contiguous.
Return the largest sum.
The subarray should contain at least one number
```
Example
For given [1, 3, -1, 2, -1, 2], the two subarrays are [1, 3] and [2, -1, 2] or [1, 3, -1, 2] and [2], they both have the largest sum 7.
```
**Challenge**
Can you do it in time complexity O(n) ?

## Solution
用数组 left 记录从左往右到 i 的最大 subarray sum (此 subarray 可以是0~i 中任何区间)

用数组 right 记录从右往左看, i - end 的最大 subarray sum (此 subarray 可以是 i~end 中任何区间)

```c++
class Solution {
public:
    // debug use
    void print_arr(vector<int> a) {
        for (auto num : a) {
            cout<<num<<" ";
        }
        cout<<endl;
    }
    /*
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    int maxTwoSubArrays(vector<int> &nums) {
        int n = nums.size();

        int min_l = min(0, nums[0]);
        vector<int> left(n, 0); // max sum array from 0-i. (could be within this range)
        int sum_l = nums[0];
        left[0] = nums[0];
        for (int i = 1; i < n; i++) {
            sum_l += nums[i];
            left[i] = max(sum_l - min_l, left[i-1]);
            min_l = min(min_l, sum_l);
        }
        // print_arr(left);

        vector<int> right(n, 0); // max sum array from i-end (could be within this range)
        int sum_r = nums[n-1];
        int min_r = min(0, nums[n-1]);
        right[n-1] = nums[n-1];
        for (int i = n-2; i >= 0; i--) {
            sum_r += nums[i];
            right[i] = max(sum_r - min_r, right[i+1]);
            min_r = min(min_r, sum_r);
        }
        // print_arr(right);

        // 0 ---- j ----- end
        int res = INT_MIN;
        for (int j = 1; j < n; j++) {
            res = max(res, left[j-1]+right[j]);
        }
        return res;        
    }
};
```

Default label
{: .label }

Blue label
{: .label .label-blue }

Stable
{: .label .label-green }

New release
{: .label .label-purple }

Coming soon
{: .label .label-yellow }

Deprecated
{: .label .label-red }
