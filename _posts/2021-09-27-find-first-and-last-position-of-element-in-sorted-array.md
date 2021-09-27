---
layout: post
title:  "Find First and Last Position of Element in Sorted Array"
author: gp
categories: [ Algorithms, Data Structures, Recursion, Binary Search, Array, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/c_scale,h_789,q_auto:eco/v1632735974/vannucherum.com/posts/2021-09-27-find-first-and-last-position-of-element-in-sorted-array/find-first-and-last-position-of-element-in-sorted-array_uz3fwt.jpg
tags: [binary-search, recursion, array, interview, algorithms, data-structures]
description: "Finding First and Last Position of Element in Sorted Array Using Binary Search Algorithm."
featured: false
hidden: false
rating: 3
---
  

Binary Search is a specialized algorithm compared to a normal sequential search. The concept of Binary Search is to search for the element very efficiently by dividing the input into two at each step thus providing O(log n) time complexity. Let's find out if we can apply this logic to find a solution for today's problem,


## The Problem

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

If the target is not found in the array, return [-1, -1].

You must write an algorithm with `O(log n)` runtime complexity.

##### Example 1
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```
##### Example 2
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

##### Example 3
```
Input: nums = [], target = 0
Output: [-1,-1]
```

## The Solution  

Looking at the problem the first method of solving that comes into our mind is to go through the array in a loop and return the index of the first occurrence and the last occurrence of the element. But the problem with that method is it will take O(n) time complexity. In the question, it's specifically mentioned that it should only take O(log n) time complexity.

So with that in mind, the potential solution we can find will be using Binary Search. Such a solution can be described as,
- Run a Binary Search to find if the element is present at least once.
- If the element is present, to find the first occurrence of the element we can do the Binary Search again in the left side part of the array to see if the element is present in that sub-array portion. - This process can be repeated until we get a -1 return that means the element isn't present in the subarray. At this point, the last known position where we found the element will be the starting position of the element in the main array.
- The above step can be repeated in the right side part of the array as well to get the last occurrence.
 
In code this solution will be,
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F02_StartEndPositionBinarySearch%2FSolution.js%23L28-L48&style=github&showBorder=on&showFileMeta=on"></script>

The code for Binary Search is,
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FRecursion%2F02_StartEndPositionBinarySearch%2FSolution.js%23L9-L21&style=github&showBorder=on&showFileMeta=on"></script>


The run time complexity of this implementation will be O(log n).

## References

- <a target="_blank" href="https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/">Find First and Last Position of Element in Sorted Array on LeetCode</a>