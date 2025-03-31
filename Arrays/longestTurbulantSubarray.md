# Longest Turbulent Subarray (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**978. Longest Turbulent Subarray**](https://leetcode.com/problems/longest-turbulent-subarray/)

---

## **Problem Statement**

Given an integer array `arr`, return the length of a **maximum size turbulent subarray** of `arr`.

A subarray is called **turbulent** if the comparison sign between each adjacent pair of elements **alternates**.

More formally, a subarray `[arr[i], arr[i + 1], ..., arr[j]]` is turbulent if and only if:

For `i <= k < j`:
- `arr[k] > arr[k + 1]` when `k` is odd, and
- `arr[k] < arr[k + 1]` when `k` is even.

OR

For `i <= k < j`:
- `arr[k] > arr[k + 1]` when `k` is even, and
- `arr[k] < arr[k + 1]` when `k` is odd.

---

## **Example 1**

**Input:**
```python
arr = [9, 4, 2, 10, 7, 8, 8, 1, 9]
```

**Output:**
```python
5
```

**Explanation:**
- Subarray `[4, 2, 10, 7, 8]` is a valid turbulent subarray.

## **Example 2**

**Input:**
```python
arr = [4, 8, 12, 16]
```

**Output:**
```python
2
```

## **Example 3**

**Input:**
```python
arr = [100]
```

**Output:**
```python
1
```

---

## **Constraints**

- `1 <= arr.length <= 4 * 10⁴`
- `0 <= arr[i] <= 10⁹`

---

## Approach & Algorithm:

- The key to solving this problem was to understand that a maximum subarray in this context means that signs are alternating i.e., `["10", "4", "5"]` --> `10 > 4 < 5`. We can see the signs were alternating and thus the maximum length of the subarray is 3.
- I've utilised a special variant of **Kadane's Algorithm** to solve this question in an efficient manner.
- I've utilised left and right pointers `leftPtr` and `rightPtr` respectively to keep track of the maximum subarray itself and shift the window accordingly.
- I use `prevSign` to keep track of the sign between two numbers from the previous iteration as a comparison tool.
- The special case is that:
  - Two numbers are equal and hence we must move the `rightPtr` ahead by 1. We then shift the `leftPtr` to one position behind `rightPtr`
  - OR the two numbers have the same comparison operators i.e., `">"` and then `">"` --> `[5, 3, 2]`. In this case we simply don't move the `rightPtr`. We then shift the `leftPtr` to one position behind `rightPtr`

## Code Implementation:

### Solution:

- **Time Complexity:** `O(n)` - We loop through the entire array.
- **Space Complexity:** `O(1)`

```python
class Solution:
    def maxTurbulenceSize(self, arr: List[int]) -> int:
        # We can use an altered Kadane's algorithm to solve this.
        leftPtr, rightPtr = 0, 1
        prevSign, maxSubArr = "", 1

        while rightPtr < len(arr):
            if arr[rightPtr - 1] < arr[rightPtr] and prevSign != "<":
                # Previous sign cannot be less than again.
                # We set 'maxSubArr' to be the size of the maximum length of subarray.
                maxSubArr = max(rightPtr - leftPtr + 1, maxSubArr)
                rightPtr += 1
                prevSign = "<"
            elif arr[rightPtr - 1] > arr[rightPtr] and prevSign != ">":
                maxSubArr = max(rightPtr - leftPtr + 1, maxSubArr)
                rightPtr += 1
                prevSign = ">"
            else:
                # The numbers are either equal or have the same comparison operations.
                if arr[rightPtr - 1] == arr[rightPtr]:
                    # Special case as numbers are equal.
                    rightPtr += 1

                leftPtr = rightPtr - 1
                prevSign = ""

        return maxSubArr
```
