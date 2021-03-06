---
title: "Climbing Stairs"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "python"]
categories: ["algorithm"]
date: 2019-08-28T15:16:10+08:00
draft: false
archive: false
---
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

#### Note Given n will be a positive integer.

### Example 1
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
### Example 2
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
### Solution
```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        # The result is observes Fibonacci sequence
        s1, s2 = 1, 2
        if n == 1:
            return s1
        elif n == 2:
            return s2
        else:
            while n > 2:
                s1, s2 = s2, s1+s2
                n -= 1
        return s2
```
or
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        if n == 2:
            return 2

        dp = [1] * n
        dp[0] = 1
        dp[1] = 2
        for i in range(2, n):
            dp[i] = dp[i-1] + dp[i-2]

        return dp[n-1]
```
