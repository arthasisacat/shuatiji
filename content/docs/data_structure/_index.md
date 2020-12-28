---
weight: 3
bookCollapseSection: true
BookToC: true
---

# Data Structure

## ?? or TODO
- [284. Peeking Iterator](284) wth???
- 
## important & classic
- [394. Decode String](394) recursive and non recursive ways. 
- [503. Next Greater Element II](503)
- [957. Prison Cells After N Days](957)
- [739. Daily Temperatures](739)
- [819. Most Common Word ](819) easy one.
- [962. Maximum Width Ramp](962)


## prefix sum
- [304](304) (2D prefix sum)
- [523. Continuous Subarray Sum](523)
- 
## segment tree
template: [304](304)

## queue, stack
- [394. Decode String](394)
- [739. Daily Temperatures](739)
- [362. Design Hit Counter](362)
- [735. Asteroid Collision](735) 3

## stack
- [907. Sum of Subarray Minimums](907) IMPORTANT!!!!
- [739. Daily Temperatures](739) classic
- [496. Next Greater Element I](496)
- [503. Next Greater Element II](503)
- [1019. Next Greater Node In Linked List](1019) good! 4
- [385. Mini Parser](385) so hard!!! 我觉得我还是不会.
- [20. Valid Parentheses](20)
- [962. Maximum Width Ramp](962) hard, stack!
- [636. Exclusive Time of Functions](636) hard!!!
- [856. Score of Parentheses](856)
- [921. Minimum Add to Make Parentheses Valid]({{< ref "921.md" >}}) easy
- [946. Validate Stack Sequences](946) 4
- [962. Maximum Width Ramp](962) !!! 5
- [1003. Check If Word Is Valid After Substitutions](1003) 2
- [1047. Remove All Adjacent Duplicates In String](1047) easy
- [1249. Minimum Remove to Make Valid Parentheses](1249)
- [71. Simplify Path](71)
- [402. Remove K Digits](402) hard
- [456. 132 Pattern](456) hard!
- [1475. Final Prices With a Special Discount in a Shop](1475) 2
- [32. Longest Valid Parentheses](32)
- [84. Largest Rectangle in Histogram](84) hard


## heap, priority_queue
- [703. Kth Largest Element in a Stream](703) easy
- [23. Merge k Sorted Lists](23)
- [295. Find Median from Data Stream](295)
- [373. Find K Pairs with Smallest Sums](373) customized heap compare function. LEARN!

 
## design structure: LRU, LFU, queue, stack...
- [146. LRU cache](146)  use `list`
- [460. LFU cache](460)
- [716. Max Stack](716) important!!! usage of `list`. Also compare this with 155
- [155. Min Stack](155) Different method from 716 because this only ask for `getMin()`
but no `popMin()`. So 2 stacks is enough. 
- [225. Implement Stack using Queues](225)
- [362. Design Hit Counter](362)
- [380. Insert Delete GetRandom O(1)](380)
- [622. Design Circular Queue](622)
- [641. Design Circular Deque](641)
- [707. Design Linked List](707)


## hash table
- [325. Maximum Size Subarray Sum Equals](325) important
- [890. Find and Replace Pattern](890)
- [290. Word Pattern](290)
- [128. Longest Consecutive Sequence](128)
- [791. Custom Sort String](791) does not look like hash table problem but it is
- [1282. Group the People Given the Group Size They Belong To](1282)
- [49. Group Anagrams](49)
- [30. Substring with Concatenation of All Words](30) 
- [966. Vowel Spellchecker](966) hard

Write hash function for `unordered_set<pair<int,int>>`: [939. mininum area rectangle](939)
```c++
struct pair_hash {
    inline std::size_t operator()(const std::pair<int,int> & v) const {
        return v.first*31+v.second;
    }
};

unordered_set<pair<int,int>,pair_hash> seen;   
```

## use data structure wisely
- [36. Valid Sudoku](36) 3.5
- [73. Set Matrix Zeroes](73)
- [119. Pascal's Triangle II](119)
- [835. Image Overlap](835) 2d to 1d, make it faster!
- [911. Online Election](911) 4, good.
- [916. Word Subsets](916) 3.5?
- [1405. Longest Happy String](1405) don't know which category this should fall into
- [1488. Avoid Flood in The City](1488)
- [119. Pascal's Triangle II](119) do it in place


## data stream
- [295. Find Median from Data Stream](295)
- [703. Kth Largest Element in a Stream](703) easy, priority_queue
- 


## array
- [228. Summary Ranges](228)
- [498. Diagonal Traverse](498) diagonally visit array
- [1424. Diagonal Traverse II](1424) diagonally visit array
- [659. Split Array into Consecutive Subsequences](659)
- [957. Prison Cells After N Days](957) 4
- [1424. Diagonal Traverse II](1424) 
- [220. Contains Duplicate III](220)
  
  
## line sweep
[218. The Skyline Problem](218) hard

## hard!
- [325](325)
- [1171. Remove Zero Sum Consecutive Nodes from Linked List](1171)
- [232. Implement Queue using Stacks](232)


## rotate image
[48. Rotate Image](48)

## loop
- [565. Array Nesting](565) 3
- [min_swaps_to_sort](min_swaps_to_sort) this is same as 565 but looks harder


## parentheses
Some are using stack, others are not. the complete list is [here](https://shuatiji.web.app/docs/notes/problems/)


## calculator
- [224. Basic Calculator](224) simpler version of 772
- [227. Basic Calculator II](227)
- [772. Basic Calculator III](772) hard!!!


## random pick
- [497. Random Point in Non-overlapping Rectangles](497)


## spiral matrix
- [54. Spiral Matrix](54)
- [59. Spiral Matrix II](59)
- [885. Spiral Matrix III](885) too hard...