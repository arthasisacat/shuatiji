---
title: 545. Top k Largest Numbers II
parent: data_structure
has_children: false
weight: 500
permalink: lintcode545
---
# 545. Top k Largest Numbers II
[lintcode link](https://www.lintcode.com/problem/top-k-largest-numbers-ii/description)

**difficulty(1-5)** 
2

**notes**   


## Description
https://www.lintcode.com/problem/top-k-largest-numbers-ii/description
Description
Implement a data structure, provide two interfaces:
add(number). Add a new number in the data structure.
topk(). Return the top k largest numbers in this data structure. k is given when we create the data structure.
```
Example
s = new Solution(3);
>> create a new data structure.
s.add(3)
s.add(10)
s.topk()
>> return [10, 3]
s.add(1000)
s.add(-99)
s.topk()
>> return [1000, 10, 3]
s.add(4)
s.topk()
>> return [1000, 10, 4]
s.add(100)
s.topk()
>> return [1000, 100, 10]
```
## Solution
没啥好说的, `priority_queue` 直接解决. 
**
side note
priority queue *一个一个插入是 n* log( n) 如果不是一个一个而是一起插入, 
则可以达到最优的 O(n)构造时间. **


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
