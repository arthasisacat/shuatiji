---
title: sort and search
weight: 4
bookCollapseSection: true
BookToC: true
---
#  Sort and Search


## TODO
- [540](540)
- [324. Wiggle Sort II](324)
- 
## quick sort and merge sort template
[template](quicksort_mergesort.md)

## Basics/Classic
- [bianry search basic](704) **binary search template**
- [153. Find Minimum in Rotated Sorted Array](153)
- [31. Next Permutation](31)
- [33. Search in Rotated Sorted Array](33)
- [81. Search in Rotated Sorted Array II](81) based on 33, but this one allows duplicates.
- [34. Find First and Last Position of Element in Sorted Array](34) basic binary search
- [35.Search Insert Position](35)
- [215. Kth Largest Element in an Array](215) quick select !!!!
- [378. Kth Smallest Element in a Sorted Matrix](378) hard, 必会!!!
- [702. Search in a Sorted Array of Unknown Size](702)
- [162. Find Peak Element](162)

## Important problem
- [lintcode404](lintcode404)

## hard ones
- [324. Wiggle Sort II](324) Super hard!
- [462. Minimum Moves to Equal Array Elements II](462) hard
- [475. Heaters](475)  Use 2 method to do it! scan and binary search!
- [528. Random Pick with Weight](528)
- [81. Search in Rotated Sorted Array II](81) tricky. 必会!
- [240. Search a 2D Matrix II](240) 4
- [414. Third Maximum Number](414) 4
- [1201. Ugly Number III](1201) 5


## quick select
- [215. Kth Largest Element in an Array](215) 
- [4. Median of Two Sorted Arrays](4)
- [462. Minimum Moves to Equal Array Elements II](462) hard

## binary search on result
- [69. Sqrt(x)](69)
- [367. Valid Perfect Square](367)
- 
## bucket sort
- [347. Top K Frequent Elements](347)
- [825. Friends Of Appropriate Ages]({{< ref "825.md" >}})
- [451. Sort Characters By Frequency](451)

## devide and conquer
- [148. Sort List](148) merge sort, hard.
- [274. H-Index](274), [275](275.md) same
- [50. Pow(x, n)](50)
- [108. Convert Sorted Array to Binary Search Tree]({{< ref "108.md" >}})


## handy lower_bound/upper_bound
- [658. Find K Closest Elements](658)
- [911. Online Election](911) 4, good.
- [74. Search a 2D Matrix](74)
- [436. Find Right Interval](436)

## weird
- [406. Queue Reconstruction by Height](406)
- [179. Largest Number](179) 3.5


## custominzed sorting function

### customized sorting function for `set<pair<int,int>>`
[link](451)

### customized sorting function for `priority_queue`
Note that the Compare parameter is defined such that it
returns true if its first argument comes before its second 
argument in a weak ordering. But because the priority queue 
outputs largest elements first, the elements that
"come before" are actually output last. That is, the front 
of the queue contains the "last" element according to the 
weak ordering imposed by Compare.

- [link](692)
- [link](23)
- [378. Kth Smallest Element in a Sorted Matrix](378) hard, 必会!!!

### customized sorting for `vector<vector<int>>`

- [link](973) (also used lambda)
