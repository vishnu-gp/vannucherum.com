---
layout: post
title:  "Minimum Remove to Make Valid Parentheses"
author: gp
categories: [ Algorithms, Data Structures, Stacks, Medium]
image: https://res.cloudinary.com/vannucherum/image/upload/v1628264324/vannucherum.com/posts/2021-08-10-minimum-remove-to-make-valid-parentheses/stacks_vvvmbh.jpg
tags: [stacks, interview, algorithms, data-structures]
description: "Solving Minimum Remove to Make Valid Parentheses Problem. Different approaches to solve the problem and their corresponding time and space complexities explained."
featured: false
hidden: false
rating: 4
---
  

Stack is another important data structure. The parentheses validity check is a classic question that can be solved using a stack. It's by pushing the opening parentheses to stack and comparing the closing parentheses with the top of the stack and popping them correspondingly. It's a relatively easier problem to solve. That's why we are trying to solve an extended version of that.


## The Problem

Given a string s of `'('` , `')'` and lowercase English characters. 
Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting parentheses string is valid and return `any` valid string.
Formally, a parentheses string is valid if and only if:
It is the empty string, contains only lowercase characters, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.

  

**Example 1:**
```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```
**Example 2:**
```
Input: s = "a)b(c)d"
Output: "ab(c)d"
```
**Example 3:**
```
Input: s = "))(("
Output: ""
Explanation: An empty string is also valid.
```
**Example 4:**
```
Input: s = "(a(b(c)d)"
Output:"a(b(c)d)"
```

## The Solution  
To solve this problem we can definitely make use of stack data structure. Like the parenthesis validation problem, we will be pushing open parenthesis to stack and compare the top of the stack with closed parenthesis. But we will do it a little differently to get the string with a valid string with minimum character removals. The step by step procedures to do while looping through the string is,

If the current character is `(` push the position of  to stack
If the current character is `)` then we check the stack's state. If the stack is empty it means that means we are encountering a closing parenthesis before seeing a corresponding opening parenthesis, so it's clear that we don't need that in the string, so we remove that and adjust the value of `i` to match with the new string length. If the stack wasn't empty then we just pop out the last opening parenthesis from the stack to match the count and move forward.
By the time we reach the end of the string if there is any opening parenthesis left in the stack that means they don't have any matching closing parenthesis in the string, so we will remove those parentheses as well from the string to get the final output.
The above logic written in JavaScript would look like,
<script src="https://emgithub.com/embed.js?target=https%3A%2F%2Fgithub.com%2Fvishnu-gp%2Falgorithm-ds%2Fblob%2Fmaster%2FExcercises%2FStacks%2F02_MinimumRemoveToMakeValidParentheses%2FSolution.js%23L5-L26&style=github&showBorder=on&showFileMeta=on"></script>

 The time complexity of this problem is O(n) and we are not using any extra scaling memory space here.

## References

- <a target="_blank" href="https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/">Minimum Remove to Make Valid Parentheses on LeetCode</a>