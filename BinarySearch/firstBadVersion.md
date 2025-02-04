# First Bad Version (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**First Bad Version**](https://leetcode.com/problems/first-bad-version/)

---

## Problem Description

You are a **product manager** and currently leading a team to develop a new product. Unfortunately, the latest version of your product **fails the quality check**. Since each version is developed based on the previous version, **all the versions after a bad version are also bad**.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to **find out the first bad one**, which causes all the following ones to be bad.

You are given an API: `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad `version`. You should minimize the number of calls to the API.

---

## Examples

### Example 1:

**Input**:
`Input: n = 5, bad = 4`

**Output**:
`Output: 4`

**Explanation**:

```
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.
```

### Example 2:

**Input**:
`Input: n = 1, bad = 1`

**Output**:
`Output: 1`

## Constraints

- `1 <= bad <= n <= 2^31 - 1`

---

## Approach & Algorithm

- The key to solving this problem was to observe that it relies on the **binary search algorithm** for searching within ranges.
- We ran the binary search algorithm on this problem but with a slight twist.
- We use the `mid` variable to indicate the current version we are testing on to see if it is a bad version as normal.
- We check if the current version (using `mid`) is a bad version **if it is** we also check the version before it (`m - 1`).
  - If the version before is **bad** as well then we know that the current version `mid` is not the first bad version. We then re-adjust our pointers.
  - If the version before is **not** bad, then we know that the current version `mid` is indeed the first bad version. We then return `mid`.

## Code Solutions

- **Time Complexity**: It is `O(log(n))`.

```python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        leftPtr, rightPtr, mid = 0, n, -1

        while leftPtr <= rightPtr:
            mid = (leftPtr + rightPtr) // 2

            if isBadVersion(mid) and not isBadVersion(mid - 1):
                # Version at mid is a bad version and version before mid
                # is NOT a bad version meaning we found the first bad version
                return mid
            elif isBadVersion(mid) and isBadVersion(mid - 1):
                # Version before mid is a bad version too
                # We must then try find the first bad version again
                rightPtr = mid - 1
            elif not isBadVersion(mid):
                # This means everything to the left of mid is also False
                # We must search toward the right of mid
                leftPtr = mid + 1
```
