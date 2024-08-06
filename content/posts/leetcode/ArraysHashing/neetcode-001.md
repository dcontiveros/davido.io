---
title: "Neetcode 1/150 - Contains Duplicate"
date: 2024-04-24T14:41:14-04:00
---

This is entry `1/150` in the NeetCode150 Challenge.

What seems like a trivial problem to solve actually led me down a blackhole of Python efficiencies. The problem states:

> Given an integer array `nums`, return true if any value appears at least twice in the array, and return false if every element is distinct.

Now obviously the problem isn't data type specific since we are using Python. There are two methods which I impemented for this, with the first being the naive one:

1. Make an empty dict
2. If the current element _IS NOT_ in the dict, insert it.
   Else, the current element _IS_ in the dict, break the loop and return True.
3. Return False if we don't find a value in the dict at all after all elements have been iterated through.

The second implementation is quite simple.

1. Convert the list into a set
2. If the length of the list is the same as the length of the set, there are no duplicates, return False.
3. Else: if they differ, return True.

Here is the code I implemented for both functions outside of Leetcode (I tested both and each pased all taste cases and counted as a submission):

```python
def contains_duplicate(nums):
    dupe_found = False
    results = {}
    for number in nums:
        if number in results:
            dupe_found = True
            print(dupe_found)
            return dupe_found
        else:
            results[number] = "Found"
    print(dupe_found)
    return dupe_found


def contains_duplicate_with_set(nums):
    if len(nums) == len(set(nums)):
        print("No Duplicates")
        return False
    else:
        print("Print Duplicate found")
        return True


# Should return True
nums_case1 = [1, 2, 3, 1]
# Should return False
nums_case2 = [1, 2, 3, 4]
# Should return True
nums_case3 = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]

# run test cases
contains_duplicate(nums_case1)
contains_duplicate(nums_case2)
contains_duplicate(nums_case3)
contains_duplicate_with_set(nums_case1)
contains_duplicate_with_set(nums_case2)
contains_duplicate_with_set(nums_case3)
```

The set execution ran more quickly on Leetcode (non premium account). I have no idea if this matters, but as I was coding the second implementation I started to wonder whether converting to a set was actually more efficient.

A `list -> set` conversion relies on `O(N)` iterations, which is essentially what the basic insert does. However, this doesn't account for _SPACE_ complexity. I started to research this and it appears sets do take up quite a bit more memory than lists with the most inefficient conversions being based around lists with a small set of numbers. The source I used was the following:

[is-python-set-more-space-efficient-than-list](https://stackoverflow.com/questions/13547883/is-python-set-more-space-efficient-than-list)

Let's use the space complexity defintion from WikiPedia:

> The space complexity of an algorithm or a data structure is the amount of memory space required to solve an instance of the computational problem as a function of characteristics of the input.

So thinking of hash tables vs. sets on the memory level, which is more efficient? I don't think it matters very much in this case because if we have a collision on the underlying structure we will automatically exit the program and return `True`. This isn't a practical problem to be worrying about but it makes good practice to start thinking about how implementations of algorithms will look on underlying hardware.

I will try in the future to make my solutions not rely on external libraries unless absolutely necessary.

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Day 1 - Contains Duplicate](https://youtu.be/rJ2NsNSexl0?si=AisiqXmq_Om49dQF)

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
