---
title: Project#1 - Buffer Pool
---

## Overview

The buffer pool is responsible for moving physical pages back and forth from main memory to disk.
It allows a DBMS to support databases that are larger than the amount of memory that is available to the system.
The buffer pool's operations are transparent to other parts in the system.

**Your implementation will need to be thread-safe.**

You will need to implement the following three components in your storage manager:

* Extendible Hash Table
* LRU-K Replacement Policy
* Buffer Pool Manager Instance

## Task #1 - Extendible Hash Table

Read in preparation:
[Extendible hashing WIKI](https://en.wikipedia.org/wiki/Extendible_hashing)

WIKI基本上告诉你怎么写了。一开始我还没搞懂`local_depth`和`gobal_depth`的区别。之后想明白了，就是树嘛。把每个桶看成一个叶子，`local_depth`是当前叶子的深度，`gobal_depth`就是树的深度，有一点点像字典树。

这里有一个点Debug了很久，在线提交一直过不去。之前认为，分裂了一次之后再次重新分配就不会出问题了，其实不是的。重分配后仍然有可能需要继续分裂。比如考虑`bucket_size`=1, 先后插入键值为1000001和键值为0000001，要分裂6次才能放入。

## Task #2 - LRU-K Replacement Policy

力扣练手[LRU 缓存](https://leetcode.cn/problems/lru-cache/)

Backward k-distance is computed as the difference in time between current timestamp and the timestamp of kth previous access.

这里回退k次的距离：从最新的一次访问倒回去k-1次的访问的时间戳之差。比如k=2，帧fram1的访问历史时间[1,3,5,6]，对于帧fram1的backward k-distance为6-5=1

 When multipe frames have +inf backward k-distance, the replacer evicts the frame with the earliest timestamp.

这里+inf 驱逐的顺序是FIFO，与随后的访问无关，只关心第一次访问的时间戳。

我的思路两个list和一个hash表

## Task #3 - Buffer Pool Manager Instance

看着注释基本上就可以了，但是细节多。`FetchPgImp`和`NewPgImp`都算一次Pin，一个页有Pin时，绝对不能被`LRUKReplacer`驱逐.

## 线程安全

加大锁🔒！！

最后成绩200开外。
