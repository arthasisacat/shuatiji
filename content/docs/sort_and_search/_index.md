---
weight: 4
bookCollapseSection: true
---
#  Sorting and Search
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Basic problems
- [bianry search basic](/docs/704)
- [153. Find Minimum in Rotated Sorted Array](/docs/153)

## use lower_bound/upper_bound for search
- [658. Find K Closest Elements](/docs/658)

## Important problem
- [lintcode404](/docs/lintcode404)
- [quick sort](/docs/quick_sort)
- [merge sort](/docs/merge_sort)

## hard ones
- [475. Heaters](/docs/475)  Use 2 method to do it! scan and binary search!
- [528. Random Pick with Weight](/docs/528)
- [378. Kth Smallest Element in a Sorted Matrix](/docs/378)

## bucket sort
[link](/docs/347)

## sort linked list
- [148. Sort List](/docs/148) merge sort, hard.

## customized sorting function for `set<pair<int,int>>`
[link](/docs/451)

## customized sorting function for `priority_queue`
Note that the Compare parameter is defined such that it
returns true if its first argument comes before its second 
argument in a weak ordering. But because the priority queue 
outputs largest elements first, the elements that
"come before" are actually output last. That is, the front 
of the queue contains the "last" element according to the 
weak ordering imposed by Compare.

[link](/docs/692)

[link](/docs/23)

[378 hard!!!](/docs/378)

## customized sorting for `vector<vector<int>>`

[link](/docs/973) (also used lambda)

## merge intervals
- [56. Merge Intervals](docs/56) easy


## TODO
[540](/docs/540)