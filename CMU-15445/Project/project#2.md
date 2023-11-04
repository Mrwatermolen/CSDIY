---
title: Project#2 - B+Tree
---

## Overview

The second programming project is to implement an index in your database system. The index is responsible for fast data retrieval without having to search through every row in a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

The correctness of B+Tree index depends on the correctness of your implementation of buffer pool, we will not provide solutions for the previous programming projects. Since the first checkpoint is closely related to the second checkpoint in which you will implement index crabbing within existing B+ index, we have passed in a pointer parameter called transaction with default value nullptr. You can safely ignore the parameter for Checkpoint #1; you do not need to change or call any functions relate to the parameter until Task #4.

[Changing compliance for zero-length arrays #151](https://github.com/cmu-db/bustub/pull/151)
