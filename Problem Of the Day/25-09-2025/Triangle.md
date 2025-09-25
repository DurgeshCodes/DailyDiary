# Triangle

**Date:** 25-09-2025  
**LeetCode Link:**  https://leetcode.com/problems/triangle/description/

---

## 📌 Problem Statement
Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

**Input:** triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]
**Output:** 11
**Explanation:** The triangle looks like:
   2
  3 4
 6 5 7
4 1 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).

**Example 2:**

**Input:** triangle = [[-10]]
**Output:** -10

**Constraints:**

- `1 <= triangle.length <= 200`
- `triangle[0].length == 1`
- `triangle[i].length == triangle[i - 1].length + 1`
- `-104 <= triangle[i][j] <= 104`

## 💡 Approach
- This is classic DP problem. 
- We take both $i$ and $i+1$ and then check which gives us the minimum. 
- next1 is taking i and next2 is taking i+1
- Base case is if $row == n$  then we return 0 , because there is no cost. 

- since we just need previous and next arrays, we can replace dp array with curr and next arrays.

## ⏱ Complexity
- Time:  $O(n^2)$
- Space: $O(n)$

## ✅ Final Solution

> Recursion 

```python
def minimumTotal(self, triangle: List[List[int]]) -> int:
        n = len(triangle)
        def solve(i,j):
            if i == n:
                return 0
            curr = triangle[i][j]
            nxt1 = curr + solve(i+1,j+1)
            nxt2 = curr + solve(i+1,j)
            return min(nxt1,nxt2)
        return solve(0,0)
```

> Tabulation

```python
def minimumTotal(self, triangle: List[List[int]]) -> int:
        n = len(triangle)
        nxt = [0 for i in range(n+1)]
        for i in range(n-1,-1,-1):
            curr = [0 for i in range(n+1)]
            for j in range(i,-1,-1):
                nxt1 = triangle[i][j] + nxt[j+1]
                nxt2 = triangle[i][j] + nxt[j]
                curr[j] = min(nxt1,nxt2)
            nxt = curr
        return nxt[0]
```

