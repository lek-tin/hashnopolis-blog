---
title: "56. Merge Intervals"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "merge", "array", "sort"]
categories: ["algorithm"]
date: 2018-08-24T02:19:05+08:00
draft: false
archive: false
---
Given a collection of intervals, merge all overlapping intervals.

### Example 1
```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```
### Example 2
```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```
### Solution
```python
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
  def merge(self, intervals):
    """
    :type intervals: List[Interval]
    :rtype: List[Interval]
    """
    intervals.sort(key=lambda x : x.start)
    merged = []

    ## [[1,3],[2,6],[8,10],[15,18]]
    for interval in intervals:
      # NO OVERLAP
      if not merged or merged[-1].end < interval.start:
        merged.append(interval)
      # merge because last interval and the current interval OVERLAP
      else:
        merged[-1].end = max(merged[-1].end, interval.end)
    return merged
```