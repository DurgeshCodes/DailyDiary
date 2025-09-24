# Fraction to Recurring Decimal

**Date:** 24-09-2025  
**LeetCode Link:**  https://leetcode.com/problems/fraction-to-recurring-decimal/description/

---

## 📌 Problem Statement
Given two integers representing the `numerator` and `denominator` of a fraction, return _the fraction in string format_.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return **any of them**.

It is **guaranteed** that the length of the answer string is less than `104` for all the given inputs.

**Example 1:**

**Input:** numerator = 1, denominator = 2
**Output:** "0.5"

**Example 2:**

**Input:** numerator = 2, denominator = 1
**Output:** "2"

**Example 3:**

**Input:** numerator = 4, denominator = 333
**Output:** "0.(012)"

## 💡 Approach
- Solve it like we do division in general. 
- maintain `res` array, `rem` as remainder . 
- maintain a `seen` hashmap to store the already seen remainder with index , to properly add index. 
- do `rem * 10` then append `rem % denominator` to res.
- if rem in seen, then at that index insert `(` and at last `)` , then break.

> Handle negatives, append $-$ (minus) if nr and dr have different symbols. 
> if nr is zero directly return zero.
## ⏱ Complexity
- Time: `O(n)`
- Space: `O(n)`

## ✅ Final Solution
```python
def fractionToDecimal(self, nr: int, dr: int) -> str:
        if nr == 0 : return "0"
        res = []
        if (nr < 0) ^ (dr < 0):
            res.append("-")
        nr,dr = abs(nr),abs(dr)
        res.append(str(nr//dr))
        rem = nr % dr
        if rem == 0: return "".join(res)
        res.append(".")
        seen = {}
        while rem:
            if rem in seen:
                idx = seen[rem]
                res = res[0:idx] + ['('] + res[idx:] + [')']
                break
            seen[rem] = len(res)
            rem = rem*10
            res.append(rem // dr)
            rem = rem % dr
        return "".join([str(d) for d in res])
```


