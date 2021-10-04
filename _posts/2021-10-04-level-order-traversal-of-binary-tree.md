---
layout: post
title:  "Level Order Traversal of Binary Tree"
author: gp
categories: [ Algorithms, Data Structures, BFS, Binary Tree, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/q_44/v1633340644/vannucherum.com/posts/2021-10-01-binary-tree-level-order-traversal/tree_gmsu7l.jpg
tags: [binary-tree, bfs, interview, algorithms, data-structures]
description: "Doing a Level Order Traversal of Binary Tree using Breadth-First Search."
featured: false
hidden: false
rating: 4
---
  

A binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child. Today we are going to discuss how to do a level order traversal of Binary Tree.


## The Problem

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

##### Example 1
<img src="https://res.cloudinary.com/vannucherum/image/upload/v1632821475/vannucherum.com/posts/2021-10-01-binary-tree-level-order-traversal/tree1_vjtk2b.jpg"/>
```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```
##### Example 2
```
Input: root = [1]
Output: [[1]]
```

##### Example 3
```
Input: root = []
Output: []
```

## The Solution  

To do a level order traversal of a binary tree, the first option would be to do a Breadth-First approach. Let's go ahead and do that on example number 1 check the output. The output for that will be [3,9,20,15,7] but the result need is slightly different which is [[3],[9,20],[15,7]]. This means that at every level during the Breadth-First Traversal, we should initialise a new array and store the elements in that level only in that array. To solve this question in such a method,
- Store the elements to the queue starting with the root.
- With each queue element processing, we find the queue length, initialise an empty array and queueCount to zero.
- Inside the queue processing while loop let's run another while to see if the element is an element from the current level of the tree. If yes it will be added to the newly created empty array or else the entire array will be added to the final result array.
 
JavaSript implementation of this will be,
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FBinaryTree%2F02_LevelOrderTraversal%2FSolution.js%23L13-L35&style=github&showBorder=on&showFileMeta=on"></script>


The run time complexity of this implementation will be O(n).

## References

- <a target="_blank" href="https://leetcode.com/problems/binary-tree-level-order-traversal/">Binary Tree Level Order Traversal on LeetCode</a>