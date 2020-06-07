---
title: 404. Subarray Sum II
parent: DP
has_children: false
weight: 5
permalink: lintcode404
---
# 404. Subarray Sum II
[lintcode link](https://www.lintcode.com/problem/subarray-sum-ii/description)

**difficulty(1-5)** 
5

**notes**   
IMPORTANT!!!!

## Description
Given an positive integer array A and an interval. Return the number of subarrays whose sum is in the range of given interval.
```
Example
Example 1:

Input: A = [1, 2, 3, 4], start = 1, end = 3
Output: 4
Explanation: All possible subarrays: [1](sum = 1), [1, 2](sum = 3), [2](sum = 2), [3](sum = 3).
Example 2:

Input: A = [1, 2, 3, 4], start = 1, end = 100
Output: 10
Explanation: Any subarray is ok.
Notice
Subarray is a part of origin array with continuous index.
```
## Solution 1: 
这道题特殊在, 没有小于零的元素.所以 prefix sum 必递增. prefix sum 最小值是第一个元素 - 0.

其实特别简单.moving window. 先求得 prefix_sum (size n+1 ). 然后从 i = 1 ~n 遍历一遍. 对于每个特定的 i (ps[i] 固定了) 我们要找 lower_bound & upper_bound 来满足:
ps[i] - ps[x] <= end 
=> ps[x] >= (ps[i] - end) 
即, 找到 index 属于[0,i)中第一个大于等于ps[i] - end 的 index. 找不到返回 i. 这是 lower_bound
2.ps[i] - ps[lower] >= start 
=> ps[y] <= (ps[i] - start)
即, 找到 index 属于[0,i)中最后一个小于等于ps[i] - start 的 index. 这是 upper_bound. 找不到返回-1.

```c++
class Solution {
public:
/*
    1. prefix sum 
    2. for fixed ps[i] (i from 1 to n), what is the range of x, that satisfies
    start <= (ps[i] - ps[x]) <= end
    let's say x's range is [a,b]
    also important note is ps is increasing array
    then 
        1. ps[i] - ps[a] <= end (lower bound)
        2. ps[i] - ps[b] >= start (upper bound)
        
    3. res += upper - lower + 1
*/
    
    /* a starts from index 0, find a that first meet : 
      ps[i] - ps[a] <= end
    */
    int get_lower_bound(vector<int>& ps, int i, int end) {
        int a = 0;
        while ((ps[i] - ps[a] > end) && a < i) {
            a++;
        }
        return a;
    }
    
    /*
    b starts from index 0, find b that last meet:
    ps[i] - ps[b] >= start
   
    b-1:
    increment b until it doesn't meet this criteria, thus we
    we need to return b-1 which is the last index that *meets criteria*
    */
    int get_upper_bound(vector<int>& ps, int i, int start) {
        int b = 0;
        while ((ps[i] - ps[b]) >= start && b < i) {
            b++;
        }
        return b-1;
    }

    /**
     * @param A: An integer array
     * @param start: An integer
     * @param end: An integer
     * @return: the number of possible answer
     */
    int subarraySumII(vector<int> &A, int start, int end) {
        int n = A.size();
        vector<int> ps(n+1);
        for (int i = 0; i < n; i++) {
            ps[i+1] = ps[i] + A[i];
        }
        
        int res = 0;
        for (int i = 1; i <= n; i++) {
            int lower = get_lower_bound(ps, i, end);
            int upper = get_upper_bound(ps, i, start);
            res += upper - lower + 1;
        }
        return res;
    }
};
```

## Solution 2: binary search 
faster
在 method 1 基础上, 既然 prefix_sum 是递增而且我们要 lower 和 upper bound, 那么很容易想到可以用二分法来找一头一尾. 具体实现上要很仔细. 
from: [link](http://massivealgorithms.blogspot.com/2017/05/lintcode-138-404-subarray-sum-iii.html)

前缀和数组二分搜索解法

非负整数 Subarray 相关题目的一个常用解法就是通过计算前缀和数组，然后利用二分搜索来找到目标。在这里，类似的思路同样适用。
举个例子，假设给定一个目标区间`[low,high]`，当我们遍历到prefixSum[i]时，我们的搜索范围为prefixSum[0,i-1]，而搜索目标有两个：
```
argminj (prefixSum[i]−prefixSum[j]≤high)
⇒argminj (prefixSum[i]−high≤prefixSum[j])

argmaxk (prefixSum[i]−prefixSum[k]≥low)
⇒argmaxk (prefixSum[i]−low≥prefixSum[k])
```
分别为第一个大于或等于`prefixSum[i] - high`的位置，即最左边的位置，以及最后一个小于或等于prefixSum[i] - low的位置，即最右边的位置。

看上去这是两种二分搜索，但这里有个小技巧，那就是把后一个条件稍稍修改，变成第一个大于或等于prefixSum[i] - low + 1的位置，等效于我们把需要找的位置往后移了一位。

这里的特殊情况值得详细分析一下。首先是要明确对于找highBound而言，我们本质上是需要找到满足限制条件的滑动窗口头部的最后一个位置，而在这里我们是间接地去达到这个要求，即找到该位置的下一位。当target已经大于搜索区间的最后一个元素后，我们直接返回len即可，因为此时滑动窗口头部的最后一个位置已经是len-1，不能再往后移动了。对于找其他情况而言，逻辑就更简单一点，初始化为0即可。

```c++
/**
 * prefix sum + binary search.
 * note that all elements in array is non-negative numbers, this means prefix
 * sum is ascending array! thus we could use binary search to find first
 * and last position that satisfies the condition.
 */
class Solution {
public:
    /**
     * @param A: An integer array
     * @param start: An integer
     * @param end: An integer
     * @return: the number of possible answer
     */
    int subarraySumII(vector<int> &A, int start, int end) {
        if (A.size() == 0) {
            return 0;
        }
        vector<int> ps(A.size()+1, 0);
        for (int i = 0; i < A.size(); i++) {
            ps[i+1] = ps[i] + A[i];
        }
        
        int res = 0;
        for (int i = 1; i <= A.size(); i++){
            cout<<"       i       "<<i<<endl;
            // [lower, upper)
            int lower_bound = find1(ps, i, ps[i] - end);
            int upper_bound = find1(ps, i, ps[i] - start + 1);
            res += ((upper_bound - 1) - lower_bound + 1);
        }
        return res;
    }

    /**
     * DEFINITION IS VERY IMPORTANT
     * known that: nums[] is ascending array.
     * return the first position x from [0,len) that nums[x] >= target
     * note that target could be larger than the largest element in nums[]
     */
    int find1(vector<int>& nums, int len, int target) {
        int start = 0; 
        int end = len - 1;
        int mid = -1;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (nums[mid] >= target) {
                end = mid;
            }
            else {
                start = mid;
            }
        }
        // start < end. nums[start] < nums[end]
        // if nums[end] < target, then from [0,len) no one qualifies.
        if (nums[len-1] < target) {
            cout<<len<<endl;
            return len;
        }
        if (nums[start] >= target) {
            cout<< start<<endl;
            return start;
        }
        else {
            cout<<end<<endl;
            return end;
        }
    }
};
```

```c++
class Solution {
public:
    /* a range [0,i-1], find a that first meet : 
     ps[i] - ps[a] <= end
     => ps[a] >= ps[i] - end (ps[] monotonically increasing)
    
    b starts from index 0, find b that **last** meet:
    ps[i] - ps[b] >= start
    => ps[b] <= (ps[i] - start)
    
    =>
    find b' that **first** meet: ps[b'] >= (ps[i] - start + 1)
    b = b' - 1
    */
    int first_ge(vector<int>& ps, int i, int target) {
        int s = 0;
        int e = i;
        while (s + 1 < e) {
            int m = s + (e - s) /2;
            if (ps[m] >= target) {
                e = m;
            }
            else {
                s = m;
            }
        }
        if (ps[s] >= target) {
            return s;
        }
        return e;
    }
    int subarraySumII(vector<int> &A, int start, int end) {
        int n = A.size();
        vector<int> ps(n+1);
        for (int i = 0; i < n; i++) {
            ps[i+1] = ps[i] + A[i];
        }
        
        int res = 0;
        for (int i = 1; i <= n; i++) {
            int lower = first_ge(ps, i, ps[i] - end);
            int upper = first_ge(ps, i, ps[i] - start + 1) - 1;
            // cout<<"i "<<i<<" ["<<lower<<","<<upper<<"]"<<endl;
            res += upper - lower + 1;
        }
        return res;
    }
};
```
binary_search
{: .label .label-yellow }