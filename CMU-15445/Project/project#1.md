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

For the first part of this project, you will build a general purpose hash table that uses unordered buckets to store unique key/value pairs.

You may not use another built-in hash table internally in your implementation. You must implement the following functions in the `ExtendibleHashTable` class:

* `Find(K, V)`
* `Insert(K, V)`: Insert the key/value pair into the hash table. If the key K already exists, overwrite its value with the new value V and return true. If the key/value pair couldn't be inserted into the bucket (because the bucket is full and the key is not updating an existing pair), do the following steps before retrying:
    1. If the `local depth` of the bucket is equal to the `global depth`, increment the `global depth` and double the `size of the directory`.
    2. Increment the local depth of the bucket.
    3. Split the bucket and redistribute directory pointers & the kv pairs in the bucket.
* `Remove(K)`
* `GetGlobalDepth()`: Return the current global depth of the entire hash table.
* `GetLocalDepth()`: Return the current local depth for the bucket which the given directory index points to.
* `GetNumbuckets()`: Return the total number of buckets allocated in the hash table.

You can make use of the provided IndexOf(K) private function to compute the the directory index that a given key hashes to. In addition, we provide a Bucket nested class that represents buckets in the extendible hash table. Finishing the TODOs of the Bucket class first by following the code documentation can make it easier for you to implement the ExtendibleHashTable APIs. But you can feel free to write your own internal class / helper functions.

You need to make sure that all operations in the hash table are thread-safe using std::mutex. It is up to you to decide how you want to protect the data structure.

## Task #2 - LRU-K Replacement Policy

You are expected to implement only the LRU-K replacement policy. You don't have to implement LRU or clock replacement policy, even if there is a corresponding file for it.

The LRU-K algorithm evicts a frame whose backward k-distance is maximum of all frames in the replacer. Backward k-distance is computed as the difference in time between current timestamp and the timestamp of kth previous access. A frame with less than k historical accesses is given +inf as its backward k-distance. When **multipe frames** have +inf backward k-distance, the replacer evicts the frame with the earliest timestamp.

The maximum size for the `LRUKReplacer` is the same as the size of the buffer pool since it contains placeholders for all of the frames in the `BufferPoolManager`. However, at any given moment not all the frames in the replacer are considered to be evictable. The size of `LRUKReplacer` is represented by the number of evictable frames. The `LRUKReplacer` is initialized to have no frames in it. Then, only when a frame is marked as evictable, replacer's size will increase.
