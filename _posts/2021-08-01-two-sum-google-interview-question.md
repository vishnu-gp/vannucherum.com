---
layout: post
title:  "Two Sum, the famous Google interview question"
author: gp
categories: [ Google, Algorithms, Data Structures, Arrays, Easy]
image: https://res.cloudinary.com/vannucherum/image/upload/v1627993442/vannucherum.com/posts/2021-08-01-two-sum-google-interview-question/google-logo_nyw3c0.webp
tags: [arrays, google, interview, algorithms, data-structures]
description: "Solving Two Sum, the famous Google interview question. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: true
hidden: false
rating: 4.5
---

I’ve thought about many ideas regarding my very first post here on vannucherum.com and decided to go ahead with this. What could be better than solving a Computer Science problem designed by Google for their tech interviews? This is an easy to solve question which would help in preparing for the big tech companies like Facebook, Amazon, Apple, Google, etc.

## The Problem

The Two sum problem can be described as follows

+ ***Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to target.***
+ ***You may assume that each input would have exactly one solution, and you may not use the same element twice.***
+ ***You can return the answer in any order.***

##### Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

##### Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```


## The Solution

The first method comes to our mind in solving this to check all the possible pairs of elements in the input array `nums` and verify their sum and if that equals the `target` we can return the corresponding indices of the array. Such a solution would look like the following:

<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Arrays/01_TwoSum/BruteForce.js?slice=7:18"></script>


Here we select an element and compare its complementing element(target minus the element) to all the other elements then repeat the process for all elements until we get the result matching. The problem with this approach is it isn't much efficient since it's going to take O(n<sup>2</sup>) run time complexity.
The real objective of this problem is to find an optimal solution that would take run time complexity relatively lower than the above method.

## The Optimal Solution
To create an optimal solution we are going to use a hash map where we store the complementing element as a key while looping through each element in the input array and check the present element is present as a key already in the hash map before adding them. If the element matches with a key in the hash map we can return the corresponding indices.

<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Arrays/01_TwoSum/OptimalSolution.js?slice=7:18"></script>

The run time complexity of this method will be O(n)

## References
<a target="_blank" href="https://leetcode.com/problems/two-sum/">Two Sum problem on LeetCode</a>

<iframe style="width:100%;" height="315" src="https://www.youtube.com/embed/XKu_SEDAykw?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>
