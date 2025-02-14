# Kth Largest Element in a Stream (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Kth Largest Element in a Stream**](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)

---

## Problem Statement

You are part of a university admissions office and need to keep track of the `k`th highest test score from applicants in real-time. This helps to determine cut-off marks for interviews and admissions dynamically as new applicants submit their scores.

You are tasked to implement a class which, for a given integer `k`, maintains a stream of test scores and continuously returns the `k`th highest test score after a new score has been submitted. More specifically, we are looking for the `k`th highest score in the sorted list of all scores.

### **Implement the `KthLargest` class:**

- `KthLargest(int k, int[] nums)`: Initializes the object with the integer `k` and the stream of test scores `nums`.
- `int add(int val)`: Adds a new test score `val` to the stream and returns the element representing the `k`th largest element in the pool of test scores so far.

---

## **Example 1**

**Input:**

```python
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
```

**Output:**

```python
[null, 4, 5, 5, 8, 8]
```

**Explanation:**

```plaintext
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);  # return 4
kthLargest.add(5);  # return 5
kthLargest.add(10); # return 5
kthLargest.add(9);  # return 8
kthLargest.add(4);  # return 8
```

## **Example 2**

**Input:**

```python
["KthLargest", "add", "add", "add", "add"]
[[4, [7, 7, 7, 7, 8, 3]], [2], [10], [9], [9]]
```

**Output:**

```python
[null, 7, 7, 7, 8]
```

**Explanation:**

```plaintext
KthLargest kthLargest = new KthLargest(4, [7, 7, 7, 7, 8, 3]);
kthLargest.add(2);  # return 7
kthLargest.add(10); # return 7
kthLargest.add(9);  # return 7
kthLargest.add(9);  # return 8
```

## Constraints

- `0 <= nums.length <= 10^4`
- `1 <= k <= nums.length + 1`
- `-10^4 <= nums[i] <= 10^4`
- `-10^4 <= val <= 10^4`
- At most `10^4` calls will be made to `add`.

---

## Approach & Algorithm

- I have utilised the `heapq` module from python to assist me with this LC problem.
- I used `heapq.heapify(nums)` to create a heap-style structure in `O(n)` time.
- I always maintained at most `k` elements in the heap. If at any point there are more than `k` elements in the heap whilst we **initialise** or **add** to the heap, I simply remove the smalleest elements (root) from the heap. This maintains a heap where we have `k` number of largest elements.
- The root has the kth largest element.

## Code Implementation

### Solution (DFS):

- **Time Complexity:** O(n \* log(k))

```python
import heapq

class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        heapq.heapify(nums)
        self.heap = nums
        self.k = k

        # We need to ennsure our heap is smaller than size 'k'.
        # We remove elements that are smaller up until we have 'k' elements remaining.
        while len(self.heap) > self.k:
            heapq.heappop(self.heap)

    def add(self, val: int) -> int:
        heapq.heappush(self.heap, val)

        if len(self.heap) > self.k:
            heapq.heappop(self.heap)

        return self.heap[0]

# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```
