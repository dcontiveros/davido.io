---
title: "Neetcode 2/150 -  Valid Anagram"
date: 2024-04-29T12:35:14-04:00
categories: ["neetcode"]
tags: ["leetcode"]
---

This is entry `2/150` in the NeetCode150 Challenge.

The task is as follows:

> Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise. An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

I realized that the code needed to conform to the following criteria:

1. The strings must be the same length.
2. The strings must use all individual letters.

We managed to get the naive implementation with the following code (function name edited for clarification):

```python
def is_anagram_naive(s: str, t: str) -> bool:
    temp_word = t
    if len(s) == len(t):
        for letter in s:
            if letter in temp_word:
                temp_word = temp_word.replace(letter, '', 1)
            else:
                print("False")
                return False
        print("True")
        return True
    else:
        print("False")
        return False
```

There is massive room for optimization here. When I looked up the solution for this problem, there were numerous solutions but what it boils down to is limiting all operations to `O(n)` capacity. Well how would we do this?

My original implementation was to use create two dicts and use them as hashmaps, iterate through each string, and perform a lookup to see if the current letter is present in the hashmap. If it is, increment the value by `1`` or if it isn't, insert the letter as the key and set the value to `1`. We would then repeat with the second string and compare the hashmaps.

This would require at most, two iterations on said strings and the comparison lookup. I used this StackOverflow page to confirm the complexities:

[What is the time complexity of comparing 2 dictionaries in python](https://stackoverflow.com/questions/57346276/what-is-the-time-complexity-of-comparing-2-dictionaries-in-python)

Since they have the same number of letters confirmed, we would not run into an edge case where it would take more than `O(n)` lookups.

Before I started coding this hashmap solution I also read an implementation in Java that uses a frequency array. This is essentially the fancy version of what I was originally wanting to use. The implementation I found is located here:

[Valid Anagram — LeetCode Java Solution](https://medium.com/techsoftware/valid-anagram-leetcode-java-solution-e497872e5970)

The only difference I wanted to make in Python was instead of checking to see if everything was zero, we could simply create two of these frequency arrays and compare them, rather than check for `0` value. We won't need to hold ALL the values, but only the letters that are found in the string. So how do I create a frequency array as quickly as possible? The answer is in the `collections` library.

Normally I'd hesitate to use additional libraries, especially since we have the hashmap to fall back on. However, there are some additional data structures that I have had little exposure to, so I figured this would be an excellent exercise. Here is the code I used:

```python
def is_anagram_optimized(s: str, t: str) -> bool:
    # iterate through s string
    s_fre = collections.Counter(s)
    t_fre = collections.Counter(t)
    if s_fre == t_fre:
        print("Is anagram")
        return True
    else:
        print("Is not anagram")
        return False
```

This is a `dict` subclass so it should just work, and it did. Here are both implementations checking the first few test cases:

```python
import collections


def is_anagram_naive(s: str, t: str) -> bool:
    temp_word = t
    if len(s) == len(t):
        for letter in s:
            if letter in temp_word:
                temp_word = temp_word.replace(letter, '', 1)
                # print(f"""Word left: {temp_word}""")
            else:
                print("False")
                return False
        print("True")
        return True
    else:
        print("False")
        return False


def is_anagram_optimized(s: str, t: str) -> bool:
    # iterate through s string
    s_fre = collections.Counter(s)
    t_fre = collections.Counter(t)
    if s_fre == t_fre:
        print("Is anagram")
        return True
    else:
        print("Is not anagram")
        return False


# case 1/2
x1 = "anagram"
x2 = "nagaram"
y1 = "rat"
y2 = "car"
is_anagram_naive(x1, x2)
is_anagram_naive(y1, y2)
is_anagram_optimized(x1, x2)
is_anagram_optimized(y1, y2)
```

The runtime was vastly improved. According to LeetCode, the stats for my first solution vs. the second are as follows:

```bash
# First Runtime
196ms
Beats 5.24% of users with Python3

# First Memory
16.94MB
Beats 64.75% of users with Python3

# Second Runtime
40ms
Beats 91.85% of users with Python3

# Second Memory
16.95MB
Beats 64.75% of users with Python3
```

Obviously, the next question I have is, "Which metric should I be focusing on?". Some rumblings on Reddit say to ignore these numbers and only focus on the actual complexity. In this case, I did manage to come to the optimized solution on my own, with a confirmation. For now, if we get to the optimized solution somewhat, we can notate and add it to our toolbox.

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Neetcode 2/150 - Valid Anagram](https://youtu.be/rJ2NsNSexl0?si=AisiqXmq_Om49dQF)

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
