---
title: "Two Sum 3/150"
date: 2024-04-30T13:55:40-04:00
---

This is entry `3/150` in the NeetCode150 Challenge.

Ah the Two Sum problem. A problem classified as "easy" that seems to be the first dip of your toe in the lake that is LeetCode. Let's get started.

The problem statement is as follows:

> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
>
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
>
> You can return the answer in any order.

I managed to get the brute force implementation of this with the following code:

```python
def two_sum_naive(nums, target):
    sol = []
    # 1. Loop through list
    # 2. grab element num
    for x in range(len(nums)):
        # 2. grab element num
        for y in range(x + 1, len(nums)):
            temp = nums[x] + nums[y]
            if temp == target:
                # add elements to list
                sol.append(x)
                sol.append(y)
                break
    print(sol)
    return sol
```

This method always guarantees a solution. It is terribly inefficient, however. The inner loop will always iterate `n-1` from the outer loop. There is room for improvement. Since I beat the timer, I technically did complete the challenge, but as always, let's improve. You never know when some interviewer will ask you for a follow up.

On looking up the optimal solution for this problem, I was astounded to see how simple it actually was. When you are under pressure to perform, some key information is definitely missed. It is important to step back and ask, "Is there anything in this situation that would reduce complexity?". The key wording in this problem is:

> You may assume that each input would have exactly one solution, and you may not use the same element twice.

The problem statement tells us that the input will always have one output, so there can only be one correct answer. A two sum problem is dependent on two numbers matching the target and expects us to return the element location of the problem. We can short circuit the problem with the following logic:

These complexities are most likely incorrect so reach out if you disagree. However, if we have multiple `O(n)` operations, we know constants do not matter. I see no indication of a possibility of `O(n^²)` but again, I am using this as refresher. Please call me out.

I was able to get the first test cases working with the following code:

```python
def two_sum_optimized(nums, target):
    hash_map = {}
    for i in range(len(nums)):
        if nums[i] in hash_map:
            return [i, hash_map[nums[i]]]
        else:
            hash_map[target - nums[i]] = i
```

This code is slightly confusing since it is so concise so let's look at it with the debugger. Let's use test case 2 as it is the most confusing.

Here is what the Python does:

- `target == 6`, `nums == [3, 2, 4]`
- An empty dict named `hash_map` is created.
- A loop is kicked off that start at `0` with upper bound of length of `nums`

First iteration:

- `i == 0`
- `if 3 in hash_map` condition fails.
- `else` is entered. We insert a `key:value` pair into our `hash_map` that looks like `3:0`.

Second iteration:

- `i == 1`
- `if 2 in hash_map` condition fails.
- `else` is entered. We insert a `key:value` pair into our `hash_map` that looks like `4:1`.

- Third iteration:

- `i == 2`
- `if 4 in hash_map` condition passes (lookup happens on key). We return a list composed of the current value of `i`(`2`) and the value that corresponds to the key `4` which in this case is `1`.

Simple right? 😐

The reason this works is that it the program is inserting key value pairs where the key is some difference taken from target at the number evaluated. If we happen to encounter a number that is already in our hashmap (which would correspond to an existing key), then we know that the current element and the value at that key in our hashmap would make the target. It's much more simple when you just add the numbers up.

I feel the two pointer solution is much easier to grasp, but unfortuanately that is not the most efficient algo. The trick is knowing that the delta value of the target minus the current elemnt will always be used in a future lookup. It is a neat trick which will most likely come into play when we get the Three Sum problem.

There was a massive difference in both of these implementations. Here are the stats:

```bash
# naive time
2070ms
Beats 9.59% of users with Python3

# naive space
17.39MB
Beats 84.27% of users with Python3

# optimized time
45ms
Beats 98.78% of users with Python3

# optimized space
18.05MB
Beats 6.36% of users with Python3
```

I had an amazing SVG picture to showcase detailing the algo with the two pointer approach, but deleted it. I ended up learning about the Goat library in Hugo so expect the blog to have "prettier" ASCII diagrams.

Unfortunately, I forgot to record the Two Sum problem attempt. Reflecting upon this the format of this challenge will be one video, per problem. This allows me to link the video to the blog post with max runtime of one hour for the videos.

Below are my profile links since I don't have the recording of this module. Enjoy!

👇

[Twitch](https://twitch.tv/Mexpat911)

[YouTube](https://www.youtube.com/@mexpat911)
