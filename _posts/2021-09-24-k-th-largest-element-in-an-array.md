---
layout: post
title:  "Kth Largest Element in an Array"
author: gp
categories: [ Algorithms, Data Structures, Recursion, Quick Select, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1632477912/vannucherum.com/posts/2021-09-24-kth-largest-element-in-an-array/quick-select_jmbhbf.jpg
tags: [recursion, quick-select, interview, algorithms, data-structures]
description: "Finding kth largest element in an array using Hoare's Quick Select Algorithm."
featured: true
hidden: false
rating: 4
---
  

Today we are going to discuss another LeetCode problem. 


## The Problem

Given an integer array `nums` and an integer `k`, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.
##### Example 1
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```
##### Example 2
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

## The Solution  

We will be using <a target="_blank" href="https://www.youtube.com/watch?v=aOhyCdxGJvY">Hoare's Quick Select Algorithm</a> to solve this problem,

- Quick Select algorithm will return kth smallest element. To adjust that with the question, we pass `n-k` as the `target index`, where n is the total number of elements of the array because (n-k)th smallest element is the kth largest element.
- The partition algorithm will divide the array into two(one with all elements less than the pivot and the other greater than the pivot) and move the pivot element to its original position when the array is sorted.
- The `pivot` will be now the kth largest element, where `k` is the position of the pivot from the right side of the array.
- We can compare our target index value with this `k` value. if the target index is greater than `k`, we will repeat the process in the right partition only and the left partition only otherwise.
- At any point, if the `k` value matches with the target index, the element will be returned.

The JavaScript implementation of the above logic is,
##### Find Target Index
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F01_FindKthLargestElement%2FSolution.js%23L55-L59&style=github&showBorder=on&showFileMeta=on"></script>

##### Quick Select Algorithm
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F01_FindKthLargestElement%2FSolution.js%23L40-L48&style=github&showBorder=on&showFileMeta=on"></script>

##### Partition Algorithm
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F01_FindKthLargestElement%2FSolution.js%23L19-L31&style=github&showBorder=on&showFileMeta=on"></script>

##### Swap Function
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F01_FindKthLargestElement%2FSolution.js%23L7-L11&style=github&showBorder=on&showFileMeta=on"></script>

 The best and average-case running time complexity of this program will be <b>O(n)</b> whereas the worst-case time complexity will be <b>O(n<sup>2</sup>)</b>

## References

- <a target="_blank" href="https://leetcode.com/problems/kth-largest-element-in-an-array/">Kth Largest Element in an Array on LeetCode</a>