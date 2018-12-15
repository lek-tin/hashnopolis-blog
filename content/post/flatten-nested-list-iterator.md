---
title: "Flatten Nested List Iterator"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "python", "iterator"]
categories: ["algorithm"]
date: 2018-11-13T20:03:07-08:00
draft: false
archive: false
---
Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**
```
Input: [[1,1],2,[1,1]]
Output: [1,1,2,1,1]
Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: `[1,1,2,1,1]`.
```
**Example 2:**
```
Input: [1,[4,[6]]]
Output: [1,4,6]
Explanation: By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: `[1,4,6]`.
```
**Solution:**
```python
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger(object):
#    def isInteger(self):
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        :rtype bool
#        """
#
#    def getInteger(self):
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        :rtype int
#        """
#
#    def getList(self):
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        :rtype List[NestedInteger]
#        """

class NestedIterator(object):
    def __init__(self, nestedList):
        """
        Initialize your data structure here.
        :type nestedList: List[NestedInteger]
        """
        arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        print(arr[::-1])
        self.flat = []
        def flatten(nested):
            for n in nested:
                if n.isInteger():
                    self.flat.append(n.getInteger())
                else:
                    flatten(n.getList())
        flatten(nestedList)
        self.flat = self.flat[::-1]

    def next(self):
        """
        :rtype: int
        """
        return self.flat.pop()

    def hasNext(self):
        """
        :rtype: bool
        """
        return bool(self.flat)

# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())
```