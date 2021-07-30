---
layout: post
title:  "Backspace String Compare Problem"
author: gp
categories: [Algorithms, Data Structures, Strings, Easy]
image: assets/images/backspace-string-compare.jpg
tags: [strings, interview, algorithms, data-structures]
description: "Solving Backspace String Compare Problem. Different approaches to solve the problem and their curresponding time and space complexities explained."
featured: true
hidden: false
rating: 3
---

So far we have solved array-based questions and discussed different solution approaches. Today we are going to try a string problem. Let's take an easy one to start with.

  

## The Problem

Given two strings `s` and `t`, return true _if they are equal when both are typed into empty text editors_. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

  

**Example 1:**
```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```
**Example 2:**
```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```
**Example 3:**
```
Input: s = "a##c", t = "#a#c"
Output: true
Explanation: Both s and t become "c".
```
**Example 4:**
```
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```
  
## The Solution

The first thing we can think about is to process the input strings to get the final compiled string and then compare them. The first part here is to process the strings, the operations involved here will be the same for both strings. That's enables us to move forward with a functional programming approach. So using the following function we can get the two input strings to a final version of the string as an array. Here what we do is,

-   Loop through the input string and initiate an extra array
-   As soon as we see a character push that to the extra array and if we see a `#` pop the last item from the same array
-   In the end, we will have the final string as an array

Let's write a function for that
<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/01_TypedOutStrings/BruteForce.js?slice=6:17"></script>

We can use the above function for the two strings and avoid code duplication using this functional programming approach. Now we have the final strings and we just need to compare the two by looping through them.


<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/01_TypedOutStrings/BruteForce.js?slice=25:36"></script>

This method will cost O(m+n) time and space complexity, where m and n are the lengths of input strings.

## The Optimal Solution

Since we already solved this question, let's now think about doing it a better way. Let's see if we can do it without taking the extra memory space for the arrays. It's better to go through the string and compare each item rather than processing it in the first place. And how we do that is the place where the critical thinking to solve this problem lies.

-   If we start from the beginning of the strings, It would create problems as there could be `#` in the places after the current position. So let's start from the end of the strings together until we reach the start of both strings.
-   If both characters at the current position of two strings are equal we move both pointers to the left to see the characters before the current position, If they are not equal it is clear that the strings are not equal and we'll stop the process there.
-   If either of the characters or one of them is a `#`, then we count that move the pointer backwards until we see an actual character. Plus when we see a character, we should move the pointer again backwards until the `#` count is zero to balance the backspaces created by `#` characters.
-   If we reach the start of both strings without seeing a mismatch our strings will be equal

The implementation of the above logic would look like

<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/01_TypedOutStrings/OptimalSolution.js?slice=7:41"></script>

The advantage of this method is it would not take the extra space complexity which was needed to store the process strings as an array. Where the time complexity remains O(m+n)

## References

- <a target="_blank" href="https://leetcode.com/problems/backspace-string-compare/">Backspace String Compare Problem on LeetCode</a>
