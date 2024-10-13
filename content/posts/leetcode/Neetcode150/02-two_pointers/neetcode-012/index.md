---
title: "Neetcode 12/150 - 3Sum"
date: 2024-10-13T19:01:41-04:00
draft: true
---

### Intro

This is entry `12/150` in the NeetCode150 Challenge.

The associated video is here: 

[Software Development | Neetcode Challenge 12/150 - 3Sum](https://youtu.be/PDfrEM1w0do)

### Status

- Difficulty: Medium
- Time restriction: ❌ 
- Test cases: ❌


### Problem

Here is the link to the Leetcode problem:

[Leetcode 15](https://leetcode.com/problems/3sum/description/)

A twist on the usual Two Sum problem.

### Root Cause Analysis

We failed both categories in this particular problem. We did not complete all test cases or solve within the time constraint. Terrible performance. 

After viewing the stream, the main issues we ran into were:

1. Dealing with duplicates
2. Too much branching
3. Not sorting in time

It is interesting that this problem does not explicitly say you can sort. Our first implementation passed about 60% of test cases, running into TLE. Then we refined it and got 308/313 test cases. We were very close. 

After we sorted, I did think of a possible solution to this problem by utilizing binary search. This was a dead end. I actually streamed two sessions trying to solve this problem, but they were irrelevant. Therefore, we uploaded the first hour and conceded to this Leetcode problem.

### Summary

We failed both categories of the problems and overengineered the solution.

### Action items

A few action items after this attempt:

1. I will no longer take multiple attempts to solve a problem. I will only use one hour max.
2. I need to implement all my sorts and searches again to ensure I have those embedded into muscle memory.
3. Do not overengineer. This includes limiting assignments and branching.
4. Practice with enumeration.
5. DO NOT RELY ON DEBUGGER!

### Final thoughts

This was the first problem I failed entirely in this section. I eventually came up with a similar algorithm to the optimal answer, but realized most of my TLEs are stemming from too many assignments and branching decisions. 

I had an interview with a well known company and received an OA of similar difficulty. However, this OA did NOT have a debugger. This is quite unrealistic for day to day, but if this is what people want, fuck it. I'm gonna give the people what they want.

I took a long break after this problem. When I researched the optimal solution and realized binary search was not part of it, but a part of a LESS optimal solution, it made me realize that I can in fact get better at this. Speaking in terms of just algos, I am starting to see the patterns in these problems. When I encounter a new problem the identification, implementation, and edge case iterative approach does seem to be working.

I want to give a scientific metric to my confidence in identification of the algorithm, but I lack the framework to express this. If I had to reduce this to probability of guessing the algorithm correclty, I would say I counld do it with more than 50% probability. However, I have not even begun to get a huge sample size for this metric, or even know more than the two algorithms from Neetcode. I recently saw a chart of the most common algorithms in job OAs "backed by data". I feel this is a bit sus, but here is the link:

[Source: AlgoMonster](https://algo.monster/problems/stats)

I do enjoy how they broke down everything via ROI. I have to admit this is a decent starting point and seeing how I'm barely tipping the first row of the chart is a bit disheartening. Just gotta keep grinding.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
