---
layout: post
title:  "Almost Valid Palindrome Problem"
author: gp
categories: [ Algorithms, Data Structures, Strings, Hard]
image: assets/images/almost-palindrome.jpg
tags: [strings, interview, algorithms, data-structures]
description: "Solving Almost Valid Palindrome Problem. Different approaches to solve the problem and their curresponding time and space complexities explained."
featured: false
hidden: false
rating: 3
---

Palindrome check problems are very common in the Strings section of the interview process. This question is a modified version of the palindrome check on a string.

  

## The Problem
Given a string `s`, return true if the string can be palindrome after deleting at most one character from it.
  

**Example 1:**
```
Input: s = "aba"
Output: true
```
**Example 2:**
```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```
**Example 3:**
```
Input: s = s = "abc"
Output: false
```
  
## The Solution

To check a string is almost palindrome, we first need to understand how to check a string is a palindrome first. There are multiple ways of doing it.
Create a copy of the string in reverse order and check all the characters in the same positions of strings are equal.
Start two different pointers one from starting of the string and another from the end of the string. Check if the character at the pointer positions. If they are matching and move the pointers together inwards step by step until they meet.
The two-pointer method can also be implemented from the middle of the string by moving pointers outwards too.

The two-pointer inward method implemented in code would look like,
<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/03_AlmostPalindrome/Solution.js?slice=7:18"></script>
Here `s` the string, `left` is the starting position and `right` is the ending position of the string.

Now to check the string is almost palindrome, we should do a process similar to the above but as soon as we see the first unmatching case, we should check if the string will become palindrome by eliminating either one of the characters at the pointer positions. Here one advantage we have is we only have to check the remaining part of the string since the other part is already verified. To write a code solution for this let's make use of the above function as well.
<script src="http://gist-it.appspot.com/https://github.com/vishnu-gp/algorithm-ds/blob/master/Excercises/Strings/03_AlmostPalindrome/Solution.js?slice=24:36"></script>

The time complexity of this solution will be O(n).

## References
-  <a target="_blank" href="https://leetcode.com/problems/valid-palindrome-ii/">Valid Palindrome on LeetCode</a>
