---
title: modular
weight: 0
---
# modular 
[wiki](https://zh.wikipedia.org/wiki/%E6%A8%A1%E9%99%A4#%E7%AD%89%E4%BB%B7%E6%80%A7)

等价性
一些取模操作，经过分解和展开可以等同于其他数学运算。这在密码学的证明中十分有用，例如：迪菲-赫爾曼密鑰交換。

恒等式：
(a mod n) mod n = a mod n
对所有的正数 x 有：nx mod n = 0
如果 p 是一个质数，且不为 b 的因数，此时由费马小定理有：abp−1 mod p = a mod p
逆运算：
[(−a mod n) + (a mod n)] mod n = 0.
b−1 mod n 表示模反元素。当且仅当 b 与 n 互质时，等式左侧有定义：[(b−1 mod n)(b mod n)] mod n = 1。
分配律：
(a + b) mod n = [(a mod n) + (b mod n)] mod n
ab mod n = [(a mod n)(b mod n)] mod n
d mod (abc) = (d mod a) + a[(d \ a) mod b] + ab[(d \ a \ b) mod c]，符号 \ 是欧几里德除法中的除法操作符，运算结果为商
c mod (a+b) = (c mod a) + [bc \ (a+b)] mod b - [bc \ (a + b)] mod a.
除法定义：仅当式子右侧有定义时，即 b、n 互质时有：
a
b
 mod n = [(a mod n)(b−1 mod n)] mod n，其他情况为未定义的。
乘法逆元：[(ab mod n)(b−1 mod n)] mod n = a mod n.