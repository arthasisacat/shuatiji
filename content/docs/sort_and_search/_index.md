---
weight: 4
bookCollapseSection: true
BookToC: true
---
#  Sorting and Search
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Basic problems
- [bianry search basic](704)
- [153. Find Minimum in Rotated Sorted Array](153)

## use lower_bound/upper_bound for search
- [658. Find K Closest Elements](658)

## Important problem
- [lintcode404](lintcode404)
- [quick sort](quick_sort)
- [merge sort](merge_sort)

## hard ones
- [475. Heaters](475)  Use 2 method to do it! scan and binary search!
- [528. Random Pick with Weight](528)
- [378. Kth Smallest Element in a Sorted Matrix](378)

## bucket sort
[link](347)

## sort linked list
- [148. Sort List](148) merge sort, hard.

## customized sorting function for `set<pair<int,int>>`
[link](451)

## customized sorting function for `priority_queue`
Note that the Compare parameter is defined such that it
returns true if its first argument comes before its second 
argument in a weak ordering. But because the priority queue 
outputs largest elements first, the elements that
"come before" are actually output last. That is, the front 
of the queue contains the "last" element according to the 
weak ordering imposed by Compare.

[link](692)

[link](23)

[378 hard!!!](378)

## customized sorting for `vector<vector<int>>`

[link](973) (also used lambda)

## merge intervals
- [56. Merge Intervals](docs/56) easy


## TODO
[540](540)