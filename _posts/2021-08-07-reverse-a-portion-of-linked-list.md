---
layout: post
title:  "Reverse A Portion of The Linked List"
author: gp
categories: [ Algorithms, Data Structures, Linked Lists, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1627998586/vannucherum.com/posts/2021-08-07-reverse-a-portion-of-linked-list/reverse-linked-list-example_xvz9bg.jpg
tags: [linked-lists, interview, algorithms, data-structures]
description: "Solving Reverse A Portion of the Linked List Problem. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: false
hidden: false
rating: 3.5
---

The linked list is another interesting data structure in Computer Science. They are similar to arrays but instead of storing data in consecutive memory locations in a linked list the data is stored anywhere in the memory and the consecutive elements are connected by storing the next elements memory address to the current element.


## The Problem
Given the `head` of a singly linked list and two integers `m` and `n` where `m` <= `n`, reverse the nodes of the list from the position `m` to position `n`, and return the reversed list.
  

**Example 1:**
<img src="https://res.cloudinary.com/vannucherum/image/upload/v1627998586/vannucherum.com/posts/2021-08-07-reverse-a-portion-of-linked-list/reverse-linked-list-example_xvz9bg.jpg">
```
Input: head = [1,2,3,4,5], m = 2, n = 4
Output: [1,4,3,2,5]
```
**Example 2:**
```
Input: head = [5], m = 1, n = 1
Output: [5]
```
  
## The Solution

To reverse a link in the linked list we have to change the link connecting from `currentNode-->nextNode` to `currentNode<--nextNode` for all the node pairs.  Here we only need to do this process on the input linked list for the nodes between `m` and `n`
Start from the first node of the linked list and move forward until the next node is the m<sup>th</sup> node.
From m<sup>th</sup> position to n<sup>th</sup> position reverse the linked list.
Finally combine the first portion, the middle portion(the reversed portion) and the last portion of the lists.

Let's write this logic into code as
<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/LinkedLists/01_ReversePartOfLinkedList/Solution.js?slice=7:29"></script>

The time complexity of this solution will be O(n).

## References
-  <a target="_blank" href="https://leetcode.com/problems/reverse-linked-list-ii/">Reverse Linked List on LeetCode</a>