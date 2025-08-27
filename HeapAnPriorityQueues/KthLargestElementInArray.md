# Kth Largest Element in an Array (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Kth Largest Element in an Array**](https://leetcode.com/problems/kth-largest-element-in-an-array/)

---

## Problem Description

Given an integer array `nums` and an integer `k`, return the **kth largest** element in the array.

- Note that it is the `k`th **largest** element in **sorted order**, not the `k`th distinct element.
- Can you solve it **without sorting**?

---

## Examples

### **Example 1**

**Input:**
```python
nums = [3,2,1,5,6,4]
k = 2
```

**Output:**
```python
5
```

## Constraints

- `1 <= k <= nums.length <= 10^5`
- `10^4 <= nums[i] <= 10^4`

## Approach & Algorithm

- I have utilised the `heapq` module from python to assist me with this LC problem.
- I have used a **max-heap** to solve this question. The root of our heap is always the largest element.
- Everytime we pop an element from the heap we are removing the largest element from it.
- So in order to comply with the specification we need to pop 'k' times from the heap to get the 'kth' largest element.

## Code Implementation

### Solution One - (DFS):

- **Time Complexity:** O(n \* log(k))

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # Create a 'max-heap'. The root of our heap will always
        # be the largest element. We can pop 'k' number of elements
        # to get the 'kth' largest element.

        maxHeap = []

        for num in nums:
            heapq.heappush(maxHeap, -num)

        count = 0
        while count < k:
            numPopped = -heapq.heappop(maxHeap)
            count += 1

        return numPopped

```

### Solution Two (Simple)

- **Note:** Same as above just slighly shorter.

- **Time Complexity:** O(n \* log(k))

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        
        while len(nums) > k:
            heapq.heappop(nums)

        heapq.heapify(nums)

        return nums[0]
```
