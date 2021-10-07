---
layout: post
title:  "Binary Tree Right Side View"
author: gp
categories: [ Algorithms, Data Structures, BFS, Binary Tree, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1633602983/vannucherum.com/posts/2021-10-07-binary-tree-right-side-view/tree_lhznnj.jpg
tags: [binary-tree, bfs, interview, algorithms, data-structures]
description: "Implementing Right Side View of a Binary Tree using Breadth-First Approach"
featured: false
hidden: false
rating: 3
---
  

Today we will discuss another Binary Tree problem.


## The Problem

Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

##### Example 1
<img src="https://res.cloudinary.com/vannucherum/image/upload/v1633602983/vannucherum.com/posts/2021-10-07-binary-tree-right-side-view/tree_lhznnj.jpg"/>
```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```
##### Example 2
```
Input: root = [1,null,3]
Output: [1,3]
```

##### Example 3
```
Input: root = []
Output: []
```

## The Solution  

The solution to this problem can be derived from the <a href="https://vannucherum.com/level-order-traversal-of-binary-tree/">Level Order Traversal</a> problem we did on Binary Tree. The only difference between Level Order Traversal and this is instead of pushing all the elements in the current level to the final array, we will only push the last element at each level. This will be the right side view of the tree.
 
Let's look at the code implementation of the above logic,
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FBinaryTree%2F03_RightSideView%2FSolutionBFS.js%23L13-L32&style=github&showBorder=on&showFileMeta=on"></script>


The run time complexity of this implementation will be O(n).

## References

- <a target="_blank" href="https://leetcode.com/problems/binary-tree-right-side-view/">Binary Tree Right Side View on LeetCode</a>