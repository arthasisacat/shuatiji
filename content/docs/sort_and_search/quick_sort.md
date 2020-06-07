---
title: quick sort
parent: sort_and_search
has_children: false
weight: 6
permalink: /docs/quick_sort
---
# Quick Sort & Merge Sort Template
```c++
class Solution {
public:
    void sortIntegers2(vector<int> &A) {
        if (A.size() == 0) {
            return;
        }
        
        // 1 quick sort
        // quick_sort(A, 0, A.size()-1);
        
        // 2 merge sort
        vector<int> tmp(A.size());
        merge_sort(A, 0, A.size()-1, tmp);
    }
    
    void merge_sort(vector<int>& A, int start, int end, vector<int>& tmp) {
        if (start >= end) {
            return;
        }
        int mid = (start + end)/2;
        merge_sort(A, start, mid, tmp);
        merge_sort(A, mid+1, end, tmp);
        
        // merge 2 parts.
        int i = start;
        int j = mid+1;
        int k = start;
        while (i <= mid && j <= end) {
            if (A[i] < A[j]) {
                tmp[k++] = A[i++];
            }
            else {
                tmp[k++] = A[j++];
            }
        }
        while (i <= mid) {
            tmp[k++] = A[i++];
        }
        while (j <= end) {
            tmp[k++] = A[j++];
        }
        
        for (int k = start; k <= end; k++) {
            A[k] = tmp[k];
        }
    }
    
    void quick_sort(vector<int>& A, int start, int end) {
        if (start >= end) {
            return;
        }
        int pivot = A[(start + end)/2];
        int i = start;
        int j = end;
        while (i <= j) {
            while (i <= j && A[i] < pivot) {
                i++;
            }
            while(i <= j && A[j] > pivot) {
                j--;
            }
            if (i <= j) {
                int tmp = A[i];
                A[i] = A[j];
                A[j] = tmp;
                i++;
                j--;
            }
        }
        quick_sort(A, start, j);
        quick_sort(A, i, end);
    }

};
```