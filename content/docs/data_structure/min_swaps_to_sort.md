---
weight: 1
title: min swaps to sort
---
# Minimum Swaps to Sort
Google phone interview problem: [lin](https://leetcode.com/discuss/interview-question/346621/Google-or-Phone-Screen-or-Min-swaps-to-sort-array)

[geekforgeek link](https://practice.geeksforgeeks.org/problems/minimum-swaps/1)

**difficulty(1-5)** 
5

**notes**   

Google interview problem

## Description
Given an array of n distinct elements, find the minimum number of swaps required to sort the array.

Examples:

Input : {4, 3, 2, 1}
Output : 2
Explanation : Swap index 0 with 3 and 1 with 2 to 
              form the sorted array {1, 2, 3, 4}.

Input : {1, 5, 4, 3, 2}
Output : 2

## Solution

solution [link](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)

其实就是找那种相互占了对方位置的loop（group）size。 每个group size - 1就是这个group归位需要的jump数目。把所有的group size -1 再加起来就好了。

```c++
int minSwaps(int A[], int N){
    vector<pair<int,int>> p;
    for (int i = 0; i < N; i++){
        p.push_back({A[i],i});
    }
    sort(p.begin(), p.end());
    
    int res = 0;
    vector<bool> visited(N, false);
    for (int i = 0; i < N; i++){
        if (visited[i]){
            continue;
        }
        int cnt = 0;
        int cur = i;
        while (!visited[cur]){
            visited[cur] = true;
            cur = p[cur].second;
            cnt++;
        }
        res += (cnt - 1);
    }
    return res;
}
```

 