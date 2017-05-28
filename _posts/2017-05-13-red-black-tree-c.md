---
layout: post
title:  "A Red-Black Tree Implementation in C"
date:   2017-05-13
author: Seth Furman
categories: programming c
---

Overview
--------
As part of my systems programming course, I completed a project that had us
implement a dynamic memory allocation library in C. Our library would manage a
given block of memory (a heap) with analogs of the standard library functions
`malloc`, `realloc`, and `free` named (respectively) `hl_alloc`, `hl_resize`,
and `hl_release`.

To make our implementation time-efficent (and for fun) I decided to implement a
Red-Black Tree (RBT), which would be used as follows:
- Each RBT node is the header of a block of memory (managed by a heap).
  + Each node contains information about the capacity of the block, the
    distance to its preceding header, and a flag indicating whether the block
    is in use (i.e. has been allocated).
- Nodes (i.e. blocks) that are in the tree are implicitly free, while those not
  in the tree are implicitly in use.
  + Note that the redundant usage status in each header is used for coalescing
    (combining adjacent free blocks).  Otherwise we would have to search the
    tree to check the usage status of each node.
- A heap's RBT is sorted by block capacity.
  + Blocks are allocated by removing the smallest free block of at least a
    given size, cleaving any extra bytes off the end (which are coalesced
    with any adjacent free blocks and returned to the tree as a new block),
    and returning the remainder.
  + Blocks are likewise freed by coalescing them with adjacent free blocks
    and adding them to the tree.

With the addition of a single pointer to keep track of the root node of a
heap's RBT, we could use this Red-Black Tree method to manage memory blocks
within the heap.

RBT Implementation
------------------
Below is the header file for my Red-Black Tree implementation, which defines
the interface. As mentioned below, the actual implementation was based on
[Professor Lyn Turbak's "Red-Black Trees" handout][turbak-rbt.pdf],
while `RBT_pretty_print` was based on an [implementation][tree-pretty-print]
written by [VasyaNovikov][vasyanovikov] (which was "inspired by the 'tree'
command in linux").

To see my full implementation and tests (which should run on either Mac OS X or
Linux) check out the GitHub repository
{% include icon-github.html username="sfurman3" %} /
[red-black-tree-c](https://github.com/sfurman3/red-black-tree-c).

```c
{% include source/rbt.h %}
```

[turbak-rbt.pdf]: /assets/documents/red-black.pdf
[vasyanovikov]: https://stackoverflow.com/users/1091436/vasyanovikov
[tree-pretty-print]: /assets/documents/tree_pretty_print_post.html
