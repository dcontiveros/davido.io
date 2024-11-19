---
title: "Neetcode 8/150 - Valid Sudoku"
date: 2024-08-10T17:09:01-04:00
categories: ["neetcode"]
tags: ["leetcode"]
---

### Intro

This is entry `8/150` in the NeetCode150 Challenge.

The associated video is here:

[Software Development | Neetcode Challenge 8/150 - Valid Sudoku](https://youtu.be/6cZn_2xKobA)

### Problem

The problem states the following:

> Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
>
> Each row must contain the digits `1-9` without repetition.
> Each column must contain the digits `1-9` without repetition.
> Each of the nine 3 x 3 sub-boxes of the grid must contain the digits `1-9` without repetition.

### Root Cause Analysis

Upon rewatching my stream, it appears that I recognized the objectives:

1. Check all rows for uniques
2. Check all cols for uniques
3. Check each subsquare for uniques

Of course, knowing how to do something and actually doing it are two different things. After inspecting my video, it appears that I was able to get both objectives 1 and 2 fairly quickly. However, objective 3 was dependent on lookups being populated by objectives 1 and 2. This is where I failed.

Looking at the Neetcode solution and various others, it appears that numerous solutions are making use of `[r][c]` lookups and doing comparisons in an iterative fashion. Nothing special really. It appears that another shortcut I did not use was skipping indices to hop to the next set of subsquares. I think I'd like to return to this problem and not use the Neetcode solution. Essentially the subbox check is where we can optimize. Most of the python solutions contain some `defaultdict()` solution. We will put this solution in our toolbox and revisit.

### Summary

I failed this solution for the following reasons:

1. Quick Index traversal to access sub squares using floor method was not accounted for
2. Failure to identify this problem as a `[r][c]` lookup exercise.

### Action items

1. Correctly identify `O(C)` solutions and try not to get phased.
2. Get better with index lookups

### Final thoughts

I don't really have much on this one. Being able to correctly identify all three objectives is good, but not being able to get the subsquares was a huge disappointment for me. Again, we will revisit this one to see if I can get a better solution.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
