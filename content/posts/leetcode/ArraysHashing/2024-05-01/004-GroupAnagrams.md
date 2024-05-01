---
title: "Group Anagrams 4/150"
date: 2024-05-01T10:15:29-04:00
---

This is entry `4/150` in the NeetCode150 Challenge.

This was the first problem where I did not reach a solution at all. The problem states:

> Given an array of strings strs, group the anagrams together. You can return the answer in any order.  
> An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Originally my thinking was as follows:

- Iterate through each `word` via loop
- Itereate through each letter in `word`
- Check the next word to ensure the length matches and all letters are present
  - If they do, add to a temp list
  - If not, move on to the next word in the nested loop to
  - repeat checks on current work
- Move onto next word

Just typing out the above algorithm made me wince. This LeetCode medium appeared to be easy, because as a human, the operation _IS_ easy. Complexity from the above algorithm requires a nested loop, and I need to iterate through EACH entry. so I am already at `O(n²)`. Regardless, I try to code a naive solution prior to optimizing. Eventually I came up with this (after three hours):

```python
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
    sol = []
    print(strs)

    # get empties and reals
    empty = 0
    real_words = []
    for word in strs:
        if not word:
            empty = empty + 1
        else:
            real_words.append(word)

    # add proper pair to solution
    print(empty)
    empty_list = []
    for x in range(empty):
        print("adding empty")
        empty_list.append("")

    # add to sol
    if empty != 0:
        sol.append(empty_list)

    for x in range(len(real_words)):
        word_list = []
        print(f"start of word list: {word_list}")
        # get cur
        cur = real_words[x]
        print(f"STARTING WORD = {cur}")
        word_in_sol = False
        if x != 0:
            # check for word
            for group in sol:
                if cur in group:
                    print(f"FOUND! SKIPPING")
                    word_in_sol = True
                    break

        if word_in_sol:
            continue
        else:
            print(f"{cur} not in SOL ... checking ...")
        # process word
        cur_dict = {}
        for letter in cur:
            if letter not in cur_dict:
                cur_dict[letter] = 1
            else:
                cur_dict[letter] = cur_dict.get(letter) + 1
        # we have a dict. Check remaining words
        for y in range(x+1, len(real_words)):
            # create dict from y
            temp_dict = {}
            for letter in real_words[y]:
                if letter not in temp_dict:
                    temp_dict[letter] = 1
                else:
                    temp_dict[letter] = temp_dict.get(letter) + 1
            if cur_dict == temp_dict:
                print("Word is an anagram")
                print(f"adding {real_words[y]} to word list")
                word_list.append(real_words[y])
        # always add original word
        word_list.append(cur)
        print(f"adding {word_list} to SOL")
        sol.append(word_list)
    print(f"SOL IS: {sol}")
    return sol
```

I received a "Time Limit Exceeded" message and called it quits. I wasn't going to get the answer in the allotted rules for my challenge. Also, the rules apply to a naive version and not getting even one solution working bothered me quite a bit.

I took a day to reflect and with no other ideas I looked up the optimal solution. The requirements are:

- Create an empty dict
- Sort each word
- Check if sorted word is in the dict
  - If the word is the dict, add the current word to the existing list that is currently the `Value` part of the `Key:Value` pair where the `Key` is the sorted word
  - If the word is `NOT` in the dict, we need to add it. The `Key:Value` pair that needs to be inserted is: `CurrentWord-Sorted: ["CurrentWord"]`

I referenced this page for the optimal lookup:

[Group Anagrams Problem (with Solution in Java, C++ & Python)](https://favtutor.com/blogs/group-anagrams)

This is actually a great approach. A sorted word will be the same everytime and negates the need for a length check. Using it as a key makes lookups on the resulting string extremely quick. Since our `Value` can be set to anything, we can just simply create a list and append, this giving us all the groupings.

Here is the code I wrote:

```python
def group_anagrams_optimized(strs):
    results = {}
    for word in strs:
        print(f"WORD: {word}")
        key = ''.join(sorted(word))
        print(f"KEY: {key}")
        if key in results:
            # We have found the key. Append the actual word to the list in value
            results[key] += [word]
        else:
            # we do not have the key in our dict, add the key:value pair
            results[key] = [word]
    # now we return a list of lists
    sol = []
    for value in results.values():
        sol.append(value)
    print(sol)
    return sol
```

This passes all test cases. Here are the stats:

```bash
# time
107ms Beats 12.50% of users with Python3
# space
19.70 MB Beats 78.37%of users with Python3
```

I also tested the list comprehension that the source material used and received much better stats:

```bash
# time
87 ms Beats 69.91% of users with Python3
# space
19.28 MB Beats 99.29% of users with Python3
```

It appears the list comprehension approach saves about 50MB and cuts down on runtime by `~19%` (`-18.69158878504673`). This is substantial for me. I will be sure to see if we can use any other list comprehensions from here on out.

I have a few thoughts on this challenge after failing my first module:

- I seriously thought I would be blazing through these. Turns out I was wrong.
- I recorded about three hours of footage prior to quitting. I read online if you don't solve these type of problems within an hour to just look up the optimal solution. After experiencing this, I agree with this opinion. All streams/recordings surrounding a Leetcode/Neetcode problem will be capped at one module and one hour. No one wants to watch three hours of failures.
- There is a pattern to all of these problems. I need to `git gud` at recognizing these patterns.
- The one video, one module limitation will ensure I do not lose any proof of this challenge. The viewers will have all of the receipts.

I stream these Neetcode problems on Twitch and have the recordings on YouTube. You can watch me attempt this module or follow me on any of the links below.

👇

[Group Anagrams](https://youtu.be/jcrVG3lmbfQ?si=sjOnptwpBpKNubkl)

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
