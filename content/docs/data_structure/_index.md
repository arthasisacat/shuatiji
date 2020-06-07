---
title: data_structure
has_children: true
weight: 3
has_toc: false
bookCollapseSection: true
---

#  Data Structure
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## time complexity

### priority_queue
If you have an array of size n and you want to build a heap from all items at once, Floyd's algorithm can do it with O(n) complexity. See Building a heap. This corresponds to the std::priority_queue constructors that accept a container parameter.

If you have an empty priority queue to which you want to add n items, one at a time, then the complexity is O(n * log(n)).

So if you have all of the items that will go into your queue before you build it, then the first method will be more efficient. You use the second method--adding items individually--when you need to maintain a queue: adding and removing elements over some time period.

Removing n items from the priority queue also is O(n * log(n)).

Documentation for std::priority_queue includes runtime complexity of all operations.

example: 

[692. Top K Frequent Words](/docs/692)

### set
std::set is commonly implemented as a red-black binary search tree. Insertion on this data structure has a worst-case of O(log(n)) complexity, as the tree is kept balanced.

### list
example problem: [](/docs/146)

std::list is a container that supports constant time insertion and removal of elements from anywhere in the container (as long as you know the iterator). Fast random access is not supported. It is usually implemented as a doubly-linked list. Compared to std::forward_list this container provides bidirectional iteration capability while being less space efficient.

Adding, removing and moving the elements within the list or across several lists does not invalidate the iterators or references. An iterator is invalidated only when the corresponding element is deleted.


## prefix sum
304 (2D prefix sum)

## segment tree
template: [304](/docs/304)

## queue, stack

- [232. Implement Queue using Stacks](/docs/232)
- [739. Daily Temperatures](/docs/739)
- [362](/docs/362)
- [962. Maximum Width Ramp](/docs/962) hard, stack!
- [735. Asteroid Collision](/docs/735) medium, interesting

## hash table
[890. Find and Replace Pattern](/docs/890)

[290. Word Pattern](/docs/290)

[128. Longest Consecutive Sequence](/docs/128)

Write hash function for `unordered_set<pair<int,int>>`: [939. mininum area rectangle](/docs/939)
```c++
struct pair_hash {
    inline std::size_t operator()(const std::pair<int,int> & v) const {
        return v.first*31+v.second;
    }
};
.
...
unordered_set<pair<int,int>,pair_hash> seen;   
```

## array
- [228. Summary Ranges](/docs/228)
- [498. Diagonal Traverse](/docs/498) diagonally visit array
- [1424. Diagonal Traverse II](/docs/1424) diagonally visit array
  
## line sweep
[218. The Skyline Problem](/docs/218) hard

## LRU, LFU...
[LRU cache](/docs/146)

[LFU cache](/docs/460)

[716. Max Stack](/docs/716) Also compare this with 155~

[155. Min Stack](/docs/155) Different method from 716 because this only ask for `getMin()`
but no `popMin()`. So 2 stacks is enough. 

## hard!
- [325](/docs/325)
- [1171. Remove Zero Sum Consecutive Nodes from Linked List](/docs/1171)

## rotate image
[48](/docs/48)

## worth looking
- [957. Prison Cells After N Days](/docs/957)