---
layout: post
title:  "Trapping Rainwater Problem"
author: gp
categories: [ Algorithms, Data Structures, Arrays, Hard]
image: https://res.cloudinary.com/vannucherum/image/upload/v1627998335/vannucherum.com/posts/2021-08-03-trapping-rain-water-problem/trapping-rainwater_x4jpad.png
tags: [arrays, interview, algorithms, data-structures]
description: "Solving Trapping Rainwater Problem. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: false
hidden: false
rating: 4
---


This is another array-based question that will be relatively harder to solve. This is similar to the <a target="_blank" href="/container-with-most-water">Container With Most Water Problem</a> which we already solved.  

## The Problem
Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.


**Example 1:**

<img src="https://res.cloudinary.com/vannucherum/image/upload/v1627998335/vannucherum.com/posts/2021-08-03-trapping-rain-water-problem/trapping-rainwater_x4jpad.png">
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```
**Example 2:**
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

## Solving The Problem 
To solve the problem let's think about the all the possible cases including edge cases,
+ [4,2,0,3,2,5] => Answer = 9
+ [2,3,2] => Answer = 0
+ [] => Answer = 0
+ [9] Answer = 0


To find the total amount of water trapped between the blocks, we need to find the amount of water trapped in all the possible places in the input array. 

For finding the water trapped at a particular index of the array, we will calculate its left maximum and right maximum which are greater than the current height then find the minimum of value from that and subtract the current height to get the final answer. That is,

Water trapped at `i`th index = *min(leftMax, rightMax) - height[i]*

If we repeat this step for all elements in the array and add up results that will be the total amount of water trapped. This is the critical thinking part of this problem

## The Solution

With the above concepts in mind let's move forward to solve this problem programmatically. So we will loop through each element of the array and find its leftMax and rightMax then add the results to the total value. This will be a brute force method and such a coding solution would look like,
<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Arrays/03_TrappingRainWater/BruteForce.js?slice=6:23"></script>

As you can see here we area looping n times in each n iteration of the array, the time complexity of this problem will be O(n<sup>2</sup>). So let's think about an optimal solution to solve this problem.


## The Optimal Solution

In this solution, we will traverse the array using a single loop and two pointers from either of the edges. We will use two pointers left and right plus visualise one of them as the current item as well. The current item will be chosen as the minimum value one. 

Now the current will be compared with its maxLeft or maxRight value to determine if water can be trapped on top of the current value. If yes, that value will be added to the total or else the max value will be updated then the pointer value is moved inwards. 

Repeating this process until the pointers meet each other would give us the total water trapped.  The following is the code solution for this.
<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Arrays/03_TrappingRainWater/OptimalSolution.js?slice=6:28"></script>

As we can see this will only iterate the array once and no nested loops are present the run time complexity of this method will be O(n)

## References
+ <a target="_blank" href="https://leetcode.com/problems/trapping-rain-water/">Trapping Rain Water on LeetCode</a>

