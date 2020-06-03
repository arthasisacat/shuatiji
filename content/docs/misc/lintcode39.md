---
title: 39.Recover Rotated Sorted Array
parent: misc
has_children: false
nav_order: 1
permalink: docs/lintcode39
---
# 39.Recover Rotated Sorted Array
[leetcode link]()

**difficulty(1-5)** 
3

**notes**   

**Challenge**

In-place, O(1) extra space and O(n) time.

时间复杂度没什么好说的. 主要是如何减小空间复杂度.
如果用 extra space, 那么太简单了.
挑战是, 如果不用extra space, 那么用"**三步反转法**"

*用 reverse(): O(1) extra space, O(n) time 的操作*

## Description
Description
Given a rotated sorted array, recover it to sorted array in-place.Have you met this question in a real interview?  YesProblem Correction
Clarification
What is rotated array?
For example, the orginal array is [1,2,3,4], The rotated array of it can be [1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]
Example
[4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]

## Solution
```c++
class Solution {
public:
    /**
     * reverse elements in nums from s to e
     */
    void reverse(vector<int>& nums, int s, int e)
    {
        while(s < e)
        {
            int tmp = nums[s];
            nums[s] = nums[e];
            nums[e] = tmp;
            s++;
            e--;
        }
    }
    /**
     * @param nums: An integer array
     * @return: nothing
     */
    void recoverRotatedSortedArray(vector<int> &nums) {
        for (int i = 0; i < nums.size(); i++)
        {
            if (nums[i] > nums[i+1]) // I assume it's rotated and have at least 2 elements
            {
                reverse(nums, 0, i);
                reverse(nums, i+1, nums.size()-1);
                reverse(nums, 0, nums.size()-1);
                return;
            }
        }
    }
};
```
