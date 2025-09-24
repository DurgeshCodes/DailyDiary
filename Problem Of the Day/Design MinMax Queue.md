# ### Design MinMax Queue

**Date:** 24-09-2025  
**Link:**  https://www.geeksforgeeks.org/problems/design-minmax-queue/1

---

## 📌 Problem Statement
Design a **SpecialQueue** data structure that functions like a normal queue but with additional support for retrieving the minimum and maximum element efficiently.  
The SpecialQueue must support the following operations:

- **enqueue(x):** Insert an element x at the rear of the queue.
- **dequeue():** Remove the element from the front of the queue.
- **getFront():** Return the front element without removing.
- **getMin():** Return the minimum element in the queue in O(1) time.
- **getMax():** Return the maximum element in the queue in O(1) time.

## 💡 Approach
> Maintain a deque to insert and delete elements.
> maintain a min queue to maintain min elements. its a deque as well. 
> maintain a max queue to maintain max elements. its a deque as well.
> min has elements stored in decreasing order. max has elements in increasing order.

> In Queues pop is done from the front. so for front we do $q[0]$ and to maintain increasing order we compare from $q[-1]$ and pop which pops from back. 

## ⏱ Complexity
- Time:  O(n)
- Space: O(n) + O(n) + O(n)

## ✅ Final Solution
```python
from collections import deque
class SpecialQueue:
    def __init__(self):
        self.q = deque()
        self.min = deque()
        self.max = deque()

    
    def enqueue(self, x):
        self.q.append(x)
        
        while self.min and self.min[-1] > x:
            self.min.pop()
        self.min.append(x)
        
        while self.max and self.max[-1] < x:
            self.max.pop()
        self.max.append(x)

    
    def dequeue(self):
        ele = self.q.popleft()
        if self.min[0] == ele:
            self.min.popleft()
        if self.max[0] == ele:
            self.max.popleft()

    
    def getFront(self):
        return self.q[0]

    
    def getMin(self):
        return self.min[0]
        # Get minimum element

    
    def getMax(self):
        return self.max[0]
        # Get maximum element
```

