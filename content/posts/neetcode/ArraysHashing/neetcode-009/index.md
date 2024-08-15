---
title: "Neetcode 9/150 - Longest Consecutive Sequence"
date: 2024-08-14T16:37:54-04:00
---

### Intro

This is entry `9/150` in the NeetCode150 Challenge.

The associated video is here: 

[Software Development | Neetcode Challenge 9/150 - Longest Consecutive Sequence](https://youtu.be/LEMfTiYWNl0)

### Problem

> Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.
> 
> You must write an algorithm that runs in `O(n)` time.

Sounds easy right? Why is this a medium? 

### Root Cause Analysis

After analyzing the recording of my performance, I can say confidently this was one of those problems that I should have thought about more logically, rather than going for naive. We managed to get `69/76` test cases before we called it quits, which is still pretty decent without getting the optimized solution. 

It seems that not knowing the time complexity of some of the more common Python operations around the ADTs Python provides is hindering me at this point. What needed to be done was:

1. Convert list to set to get rid of duplicates
2. Perform lookups on this set given a current element and keep track of those results

When I read the solution to the problem, I was pretty amazed as to why the solution would work. When I wrote the solution, it was clear that this was merely a practical `set()` operation problem.

### Summary

I failed for the following reasons:

1. Not knowing that converting to set is `O(n)`
2. Not even realizing that `set()` lookup is `O(1)` on average - [Source](https://www.geeksforgeeks.org/internal-working-of-set-in-python/)
3. Not having enough intuition that a while loop that that is broken will not be `O(n^2)`

### Action items

To mitigate this, I need to do the following:

1. Really think about whether or not a subloop will be `O(n^2)`
2. Know the time complexity of specific Python operations
3. Drill on said complexities so in case I need to do a conversion on an OA, I can operate within the constraints

### Final thoughts

Coding the final solution was straightforward. I seem to be getting a sense that I need to do more preparation prior to attempting a solution. The goal is to get mediums within `40m`, so we need to be on top of our game on other programming aspects. 

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
