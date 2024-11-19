---
title: "Neetcode 13/150 - Container With Most Water"
date: 2024-10-14T09:24:07-04:00
categories: ["neetcode"]
tags: ["leetcode"]
---

### Intro

This is entry `13/150` in the NeetCode150 Challenge.

The associated video is here:

[Software Development | Neetcode Challenge 13/150 - Container With Most Water" ](https://youtu.be/V8zPzv0gvYA)

### Status

- Difficulty: Medium
- Time restriction: ❌
- Test cases: ✅

### Problem

Here is the link to the Leetcode problem:

[Leetcode 11](https://leetcode.com/problems/container-with-most-water/description/)

Confusing af diagram.

### Root Cause Analysis

We managed to get this problem eventually once we realized that the area of the box was denoted by both the height and the distance of where the two pointers were located. We managed to get most of the test cases solved but kept running into TLE.

Upon looking at the optimal solution, it was obvious we made an error in calculation. We only had to modify a few lines of the algo, with most of them being removals. I decided to give myself the credit for this one.

### Summary

We managed to solve this problem with minimal edits to get optimal. However, we did not pass the time constraint.

### Action items

1. None. We correctly identified the use of `max()` function to keep track of the area.

### Final thoughts

It is interesting that the actual setup of the pointers is no longer the issue I am running into. I am constantly seeing that the code is starting to become the means to the solution vs. the code BEING the solution. I know that sounds like a ridiculous statement, but after rewatching the video, I realize that I have about 80% of the solution.

I am also finding it much simpler to think in terms of optimal solutions.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
