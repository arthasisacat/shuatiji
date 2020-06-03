---
title: ring_buffer
parent: data_structure
has_children: false
nav_order: 1
permalink: /docs/ring_buffer
---
# Ring Buffer

## Method 1
Example:  k = 4, arr.size() = k + 1 = 5

- w >= r
  
| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| x | d | d | d | x |
|---|---|---|---|---|
|   | r |   |   | w |

`len = w - r`

- w < r

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| d | x | x | d | d |
|---|---|---|---|---|
|   | w |   | r |   |

`len = arr.size() - r + w //< note here it's arr.size() NOT k!!!`

**when it's full?**

len = k = arr.size() - 1

**when it's empty?**

len = 0

**BIG FAT NOTE**
用此办法的话就是废一个 arr 中的格子,来处理 full 的情况.

=====
if we use `uint w; uint r` && size = 2^n 

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| d | x | x | x | x | d | d | d |
|---|---|---|---|---|---|---|---|
|   | w |   |   |   | r |   |   |

```
len = (w - r) & (size - 1) 
    = (1 - 5) & 0111 
    = (-4) & 0111
       |
        ---(use 2's complement) 4: 0100 , -4:1011+1 = 1100
    = 1100 & 0111
    = 0100(b) = 4(d)
```

## method 2
add a variable to keep track of the length by having an enqueue function to 
increment the `len` and a deque function to decrement it. This trades a variable
for a position in the buffer.

## leetcode problem 

[docs/622](docs/622)

