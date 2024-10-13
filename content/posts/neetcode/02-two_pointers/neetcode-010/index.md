---
title: "Neetcode 10/150 - Valid Palindrome"
date: 2024-10-08T09:23:17-04:00
---

### Intro

This is entry `10/150` in the NeetCode150 Challenge.

The associated video is here: 

[Software Development | Neetcode Challenge 10/150 - Valid Palindrome](https://youtu.be/PkuijMeS6-Y)

### Status

- Difficulty: Easy
- Time restriction: ❌
- Test cases: ✅

### Problem

I'm going to start linking the Leetcode problem, as some may not have premium:

[Leetcode 125](https://leetcode.com/problems/valid-palindrome/description/)

The problem requires us to check if a string (only alphanumeric characters) is a valid palindrome. We are required to use the two pointers algorithm.

### Root Cause Analysis

Some improvements from previous streams that I've incorporated is explaining my thought process prior to coding. This has helped tremendously in organizing my thoughts and code. The delay in solving this problem mainly came from figuring out the proper regular expression to sanitize the string. Once we had that, it was just a matter of grabbing edge cases.

It is interesting that some regex libraries may take other interpretations of shorthand regex. I ran into issues sanitizing `_` and `.` within my code. This was solved by using regex groups. Sanitizing strings is an essential skill and knowing the different regex patterns across engines is necessary.

### Summary

We solved all test cases but took more than the time allocation due to regex shuffling. 

### Action items
1. Practice Regex in Python.
2. Know that `while True` will ALWAYS run the code within a while loop.

### Final thoughts

Before attempting any two pointers problems, I took some boilerplate code from ChatGPT and used that to practice manipulating the pointers prior to coding any challenges. This was the only prerequisite on the Neetcode website.

> Give me two sorted integer lists so I can practice two pointers approach

I should have just used [Random.org](https://random.org) to generate the numbers but alas, I did not think of that in the moment. I stated I would do any prerequisite upskilling prior to attempting a module in the Arrays and Hashing retrospective post. Actually doing the practice has solidified this particular algorithm in my head. 

It's two pointers(☝️☝️) though, so I don't feel too much of a confidence boost. We will see how the other exercises go.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
