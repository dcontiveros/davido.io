---
title: "Neetcode 5/150 - Top K Frequent Elements"
date: 2024-08-06T00:37:27-04:00
---

This is entry `5/150` in the NeetCode150 Challenge.

The problem states:

> Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

This post is going to be a bit different. I figured out all of Neetcode solutions are going to be posted. There are videos that walk you through the most optimal strategy for solving the problem. Therefore, I have decided to post a bit more of what I am thinking and the deficiencies in my thought process. We will focus a bit less on the code.

Before coding was started, I understood that we needed to get a key-value data type that gave us each number as well as the number of occurances of said number in each list. The mistake that occured, which made me fail the problem set, was HOW to obtain this data structure.

Here are the things I tried:
1. Iterating through the list and inserting into hashmap using the `NUMBER: OCCURANCES` format ❌️
2. Various algos to sort dictionaries by values vs. keys ❌️
3. Using `Counter` from `Collections` ✅️

The `Counter` description states: 

> dict subclass for counting hashable objects

Once we converted the list to a `Counter`, it was simply a matter of returning the `k` number of elements from the `Counter`, dependent on order (ascending or descending) and extracting the actual number from the tuple pair.

I took a look at the code I submitted and it appears that it is quite simple. Here was my submission:

```python
import collections

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        ans = []
        occurrence = Counter(nums).most_common(k)
        print(occurrence)
        for x in range(k):
            ans.append(occurrence[x][0])
        
        print(ans)
        return(ans)
```

After researching this problem, it appears that most of the alternate solutions rely on one of the following implementations:

1. Bucket sort
2. Heap

I used the internal tooling of `Counter` to sort, but let's say I did not have this available. The algorithm would need significant retooling after I computed each element and their level of occurance.  I would probably go with heap in this case (another tree based ADT I need to review). As long as we can get all elements and their occurances, we can optimize on that dataset.



I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.


👇

[Neetcode 5/150 - Contains Duplicate](https://youtu.be/sp2OIW76w_s)

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
