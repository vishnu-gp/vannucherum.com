---
layout: post
title:  "Longest Substring Without Repeating Characters"
author: gp
categories: [ Algorithms, Data Structures, Strings, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1627998466/vannucherum.com/posts/2021-08-05-longest-substring-without-repeating-characters/sliding-window-problem_sk9wx3.jpg
tags: [strings, interview, algorithms, data-structures]
description: "Solving Longest Substring Without Repeating Characters Problem. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: false
hidden: false
rating: 4
---

Today, I'm going to try to solve another string problem which is a medium complex problem from LeetCode.
  
## The Problem

Given a string `s`, find the length of the longest substring without repeating characters.

**Example 1:**
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
**Example 2:**
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
**Example 3:**
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

```
**Example 4:**
```
Input: s = ""
Output: 0
```
  
## The Solution

Coming up with a brute force solution is also a part of critical thinking to solve any problem. If we loop closely to the problem statement, it's very easy to write such a solution.
Loop through each character in the string.
During each iteration, loop through the remaining characters until there is a character that is already present in the string.
Compare and store the max length from the length of all such strings
To remember the characters we will use a hash map as cache.
In code, this would look like,
<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/02_LongestSubstring/BruteForce.js?slice=6:23"></script>

As with most of the brute force solutions, this is also an O(n<sup>2</sup>) solution and that insists to think about a better solution.

## The Optimal Solution

To solve this problem in an efficient way, we are going to use a technique called **Sliding Window**.  For this we make use of two pointers left and right starting from the beginning of the string and move the pointers according to what we see next. Visually it would look like a window that we slide over the string while focusing on getting the maximum possible length substring.
Both pointers left and right start from the beginning of the string.
Move the right pointer one step to the right until we see a repeating character while tracking the maximum possible lengths.
If we see a repeating character we will move the left pointer to the point next we saw it last time in addition to moving the right pointer.
We repeat this process until the right pointer reaches the end of the input string.
To make this happen, this time we will have to store the position of strings as well well in the hash map.
Let's see how to write such a code implementation.
<script src="https://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/02_LongestSubstring/OptimalSolution.js?slice=6:21"></script>

With this, we have solved the longest substring problem very efficiently with a run-time complexity of O(n).

## References
  
- <a target="_blank" href="https://leetcode.com/problems/longest-substring-without-repeating-characters/">Longest Substring Without Repeating Characters on LeetCode</a>
