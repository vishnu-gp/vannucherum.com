---
layout: post
title:  "Flatten a Multilevel Doubly Linked List"
author: gp
categories: [ Algorithms, Data Structures, Linked Lists, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1628062785/vannucherum.com/posts/2021-08-08-flatten-a-multilevel-doubly-linked-list/thumb.png
tags: [linked-lists, interview, algorithms, data-structures]
description: "Solving Flatten a Multilevel Doubly Linked List Problem. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: false
hidden: false
rating: 4
---
  

We have already familiarised ourselves with linked lists and today we'll try to solve another linked list problem.


## The Problem

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.

  

**Example 1:**

```
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]

Output: [1,2,3,7,8,11,12,9,10,4,5,6]
```

##### Explanation

The multilevel linked list in the input is as follows:
<img src="https://res.cloudinary.com/vannucherum/image/upload/v1628062863/vannucherum.com/posts/2021-08-08-flatten-a-multilevel-doubly-linked-list/example.png">

After flattening the multilevel linked list it becomes:
<img src="https://res.cloudinary.com/vannucherum/image/upload/v1628062887/vannucherum.com/posts/2021-08-08-flatten-a-multilevel-doubly-linked-list/example_output.png">

  

**Example 2:**

```
Input: head = [1,2,null,3]

Output: [1,3,2]

Explanation: The input multilevel linked list is as follows:

1---2---NULL
|
3---NULL
```

## The Solution

  

Doubly linked lists will have two pointers one pointing to the next node and the other pointing to the previous node. This setup allows us to traverse forward and backwards in a linked list. So when we merge a multi-level doubly linked list into a single level one, we should take care of both pointer connections in every node. To do this process our approach will be

-   Start from the first node of the linked list and move forward until we reach a node with a child.
-   We'll set the child node as next while keeping a reference of the original next node as the tail part of the current level.
-   This tail can be reattached to the back of the linked list once all merges in the levels up to that level are completed.
-   We repeat this process until we reach the end of the first level of the linked list.
-   Note that while changing the links we take care of both the pointers next and prev

  

The above logic in code would look like,

<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/LinkedLists/02_FlattenMultiLevelDoublyLinkedList/Solution.js?slice=15:39"></script>

  

The worst-case time complexity of this solution will be O(n)

  

## References

- <a target="_blank" href="https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/">Flatten a Multilevel Doubly Linked List on LeetCode</a>