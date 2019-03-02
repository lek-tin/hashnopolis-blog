---
title: "Maximum Subarray"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "dynamic-programming", "kadanes-algorithm"]
categories: ["algorithm"]
date: 2019-02-20T22:30:14-08:00
draft: false
archive: false
---
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

### Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
### Follow up:
If you have figured out the `O(n)` solution, try coding another solution using the divide and conquer approach, which is more subtle.

### Solution:
Iterative:
```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }

        int[] mem = new int[nums.length];
        mem[0] = nums[0];
        int max = nums[0];
        for (int i = 1; i < nums.length; i++) {
            mem[i] = mem[i-1] > 0 ? mem[i-1] + nums[i] : nums[i];
            max = Math.max(mem[i], max);
        }

        return max;
    }
}
```
Divide and conquer
```java