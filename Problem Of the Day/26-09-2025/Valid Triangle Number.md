# Valid Triangle Number

**Date:** 26-09-2025  
**LeetCode Link:**  https://leetcode.com/problems/valid-triangle-number/description/

---

## 📌 Problem Statement
Given an integer array `nums`, return _the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle_.

**Example 1:**
**Input:** nums = [2,2,3,4]
**Output:** 3
**Explanation:** Valid combinations are: 
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3

**Example 2:**
**Input:** nums = [4,2,3,4]
**Output:** 4

**Constraints:**
- `1 <= nums.length <= 1000`
- `0 <= nums[i] <= 1000`

## 💡 Approach
> Property of triangle is sum of two sides should be strictly greater than the third side. So for each pair a, b, c one needs to check all three cases for a triangle to be valid. but if a < b < c then you just need to check a + b < c.

> **Naive approach :** 

- Sort the array. run nested for loops for i,j,k count valid a + b < c. T.C = $O(n^3)$

> **Better Approach :**

- Sort array.
- iterate in reverse, k from n-1 to 0.
- take i = 0 and j = k-1.
- while i < j, loop if a+b <=c, then need to increase i.
- else res = j - i (because all elements will satisfy for j) also do j -= 1.
- return res. 

## ⏱ Complexity
- Time: $O(n^2)$
- Space: O(1)

## ✅ Final Solution

```python
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        res = 0
        n = len(nums)
        for k in range(n-1,-1,-1):
            i,j = 0,k-1
            while i < j:
                if nums[i]+nums[j] <= nums[k]:
                    i += 1
                else:
                    res += j - i
                    j -= 1
        return res
```

