
# Generate Binary Numbers

**Date:** 25-09-2025  
**LeetCode Link:**  https://www.geeksforgeeks.org/problems/generate-binary-numbers-1587115620/1

---

## 📌 Problem Statement
Given a number **n**. The task is to generate all **binary numbers** with decimal values from **1 to n**.

**Examples:**

**Input:** n = 4
**Output:** ["1", "10", "11", "100"]
**Explanation:** Binary numbers from 1 to 4 are 1, 10, 11 and 100.

**Input:** n = 6
**Output:** ["1", "10", "11", "100", "101", "110"]
**Explanation:** Binary numbers from 1 to 6 are 1, 10, 11, 100, 101 and 110.

**Constraints:**  
$1 ≤ n ≤ 10^6$
## 💡 Approach
- I thought of using simple approach for each number generate binary and then loop and return. 
- To generate binary, loop till n is greater than 0.
- In result array append $n \% 2$
- update n to $n//2$

> Better Approach

- We can use BFS.
- in a queue append 1. 
- loop till n, popleft from queue, push the current to result. 
- in the queue append $curr + "1"$ and $curr + "0"$

## ⏱ Complexity
- Time: $O(nlogn)$ for the basic approach. $O(n)$ for the BFS
- Space: O(n) in both case.

## ✅ Final Solution

```python
 def getBinary(self,n):
        place = 0
        res = []
        while n > 1:
            rem = n%2
            n = n // 2
            res.append(str(rem))
        res.append(str(n))
        return "".join(res[::-1])
    def generateBinary(self, n):
        return [self.getBinary(i) for i in range(1,n+1)]
```


```python
 def generateBinary(self, n):
        q = deque(["1"])
        res = []
        for i in range(n):
            curr = q.popleft()
            res.append(curr)
            q.append(curr + "0")
            q.append(curr + "1")
        return res
```

