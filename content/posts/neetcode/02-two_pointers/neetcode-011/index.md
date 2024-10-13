---
title: "Neetcode 11/150 - Two Sum II - Input Array Is Sorted"
date: 2024-10-08T09:51:27-04:00
---

### Intro

This is entry `11/150` in the NeetCode150 Challenge.

The associated video is here: 

[Software Development | Neetcode Challenge 11/150 - Two Sum II - Input Array Is Sorted](https://youtu.be/oQzlcwO5c9s)

### Status

- Difficulty: Medium
- Time restriction: ❌
- Test cases: ✅

### Problem

Here is the link to the Leetcode problem:

[Leetcode 167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

This problem deals with the usual Two Sum problem, but with a twist this time. Using the two pointers algorithm is **NOT** the twist.
 
### Root Cause Analysis

We managed to pass all the test cases, possibly in a nonoptimal format. The first couple of test cases were fairly simple. Then we ran into issues with duplicate entries.

At first, I was under the impression we could just drop duplicate entries in the list into a set, and then convert that set back to a list. However, the test cases require a specific ` (index + 1) ` return format, so I immediately had to shelve this implementation. We also had a test case with a MASSIVE list to iterate through, so it looked like I was done for.

I told myself I would give myself ten minutes to think and I realized that to iterate through duplicates, I should move both pointers FIRST, then iterate once the pointers were set to the correct nonduplicate entry. This would ensure the actual positions would be reflected and I could just break once I found the target. I also noticed the following blurb on the problem set:

> EACH TEST CASE HAS A UNIQUE SOLUTION

That's big. That essentially means to me that it makes detecting a test case with a nonworking solution is not necessary. 

After I figured out the iteration of the left pointer, I then ran into an edge case where the target was the sum of the index where the left pointer was defined and the index to its left. This took me another few minutes to think about and it seems this case needs to be checked for.

I implemented the check, then passed the test case, hit submit, and to my surprise my solution worked.

All test cases passed.

Then I got a raid on Twitch, as soon as I hit the stop streaming button. 

WTF.

### Summary

We solved all test cases but took more than the time allocation due to dealing with duplicates. 

### Action items

1. Learn the most optimal way to perform this. I believe the optimal way is with multiple arrays. I will update this post for sure.
U. Turns out that the optimal solution still requires two pointers with no advancement. In case of a duplicate, I would assume you would just advance the pointer to the next index.
2. Always ask myself about duplicate entries when we run into these problems. Can we reduce? If not, we need to exclude in the fastest manner. 

### Final thoughts

I am shocked I got this, even with nonoptimal and the time constraint elapsing. It was fairly late and I did lose a little hope, but we got it.

### Stream info

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
