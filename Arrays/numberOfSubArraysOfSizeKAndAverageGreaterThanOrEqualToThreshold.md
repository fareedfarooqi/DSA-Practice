# Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**1343. Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold**](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)

---

## **Problem Statement**

Given an array of integers `arr` and two integers `k` and `threshold`, return the **number of subarrays of size `k`** where the **average is greater than or equal to `threshold`**.

---

## **Example 1**

**Input:**
```python
arr = [2, 2, 2, 2, 5, 5, 5, 8]
k = 3
threshold = 4
```

**Output:**
```python
3
```

**Explanation:**
The subarrays `[2, 5, 5]`, `[5, 5, 5]`, and `[5, 5, 8]` have averages `4`, `5`, and `6`, respectively.
All other subarrays of size 3 have averages less than 4.

## Example 2

**Input:**
```python:
arr = [11, 13, 17, 23, 29, 31, 7, 5, 2, 3]
k = 3
threshold = 5
```

**Output:**
```python
6
```

**Explanation:**
The first 6 subarrays of size 3 all have averages greater than or equal to 5.
Note: averages do not have to be whole numbers.

## Constraints

- `1 <= arr.length <= 10⁵`
- `1 <= arr[i] <= 10⁴`
- `1 <= k <= arr.length`
- `0 <= threshold <= 10⁴`

---

## Approach & Algorithm

- Both solutions below use some form of the sliding window algorithm.
- **Solution One** is signficantly faster than **Solution Two**.
- In solution one, one major optimisation in solution one is that we only use the `sum()` function once at the start of the function as opposed to running the function every iteration. Running the `sum()` function during each iteration is a costly operation `O(n)` each time. Instead of summing the entire window each time we can simply take the `windowSum` we had initially and during each iteration we can subtract the leftmost value in the window and add the rightmost new value to the `windowSum`. We can then find the new average and see if it is greater than the threshold. If it is we increment `count`.
- Solution two utilises two pointers whereby we adjust the window and find the average (by summing the window) each iteration while looping over the entire array passed in.

## Code Implementation

### Solution One (Faster):

- **Time Complexity:** O(n)

```python
from collections import deque

class Solution:
    def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
        count = 0
        windowSum = sum(arr[:k])

        if windowSum / k >= threshold:
            count += 1

        # We now need to start looping from kth value.
        for i in range(k, len(arr)):
            # We must now slide the window.
            # Note that arr[i - k] refers to the left pointer and arr[i] is the right pointer.
            windowSum = windowSum - arr[i - k] + arr[i]
            
            if windowSum / k >= threshold:
                count += 1
            
        return count
```

### Solution Two (Slower - TLE):

- **Time Complexity:** O(n * k)

```python
from collections import deque

class Solution:
    def numOfSubarrays(self, arr: List[int], k: int, threshold: int) -> int:
        subArrQueue = deque()
        L = 0
        subArrCount = 0

        # We can do it in one-pass. Remember that subarrays are contiguous.
        for R in range(len(arr) + 1):
            if len(subArrQueue) == k and (sum(subArrQueue) / len(subArrQueue) >= threshold):
                # Our subarray is full and we have found a subarray that has average > threshold.
                subArrCount += 1
                L += 1
                subArrQueue.popleft()
                
                if R < len(arr):
                    subArrQueue.append(arr[R])

                continue
            
            if R - L + 1 <= k:
                # Window limit has not yet been reached.
                subArrQueue.append(arr[R])

                continue

            if R - L + 1 > k and R < len(arr):
                # We have gone out of the window.
                L += 1
                subArrQueue.popleft()
                subArrQueue.append(arr[R])

        return subArrCount
```