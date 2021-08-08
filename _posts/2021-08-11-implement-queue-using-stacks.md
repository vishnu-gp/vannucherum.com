---
layout: post
title:  "Implementing Queue using Stacks"
author: gp
categories: [ Algorithms, Data Structures, Stacks, Queues, Easy]
image: https://res.cloudinary.com/vannucherum/image/upload/v1628411590/vannucherum.com/posts/2021-08-11-implement-queue-using-stacks/q.jpg
tags: [stacks, queues, interview, algorithms, data-structures]
description: "Implementing a queue data structure using two stack data structures."
featured: true
hidden: false
rating: 4
---
  

We have done some problems using stack and today we are trying to do more of a conceptual exercise. 


## The Problem

Implement a queue data structure using stacks.

## The Solution  

To solve this, let's try to understand the difference between stack and queue,
- Stack: Elements are inserted and deleted from the top of the stack. Follows LIFO(Last In First Out) meaning the last inserted element will be the one coming out first.
- Queue: Elements are inserted at the end of the queue and deleted from the front of the queue. Follows FIFO(First In First Out) meaning the first inserted element will be coming out first.

To implement a queue using stacks,
- We need two stacks. We name it `in` and `out`
- Insertions will always happen at the top of the stack `in`
- Deletions will always happen at the top of the stack `out` by moving all elements of `in` to `out` before deletion

This way it will be a FIFO data structure using two stacks which works as LIFO. Let's see the JavaScript Class implementation of this logic,
<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Queues/01_ImplementQueueUsingStacks/QueueWithStacks.js"></script>

 One disadvantage of implementing a queue using stacks is the increase in the time complexity of `dequeue` and `peek` operations. Originally operations `enqueue`, `dequeue` and `peek` operations will only take O(1) time complexity but when we implement it using stacks due to the limitations in the stack `dequeue` and `peek` operations will take O(n) time complexity.

## References

- <a target="_blank" href="https://leetcode.com/problems/implement-queue-using-stacks/">Implement Queue using Stacks on LeetCode</a>