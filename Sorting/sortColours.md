# Sort Colors (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Sort Colors**](https://leetcode.com/problems/sort-colors/description/)

---

## **Problem Statement**

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order **red, white, and blue**.

We will use the integers **0, 1, and 2** to represent the colors **red, white, and blue**, respectively.

You must solve this problem **without using the library's sort function**.

---

## **Example 1**

**Input**:

```python
nums = [2,0,2,1,1,0]
```

**Output**:

```python
[0,0,1,1,2,2]
```

## **Example 2**

**Input**:

```python
nums = [2,0,1]
```

**Output**:

```python
[0,1,2]
```

## **Constraints**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.

---

## **Follow-up**

Could you come up with a **one-pass algorithm** using only **constant extra space**?

---

## Approach & Algorithm

- We could have utilised **any** sorting algorithm on this question. But my goal was to utilise the most **efficient** algorithm.
- The key to notice in this question is that the range of input numbers is very small so we can use **Bucket Sort (Counting Sort)** Algorithm.
- Idea of this algorithm is that we will create a `counts` array that will keep track of how many times a number from `nums` array has occurred.
- Note it is based on the index, for example if `nums = [2, 1, 2, 0, 1, 0]`, then `counts = [2, 2, 2]`, so the index in count represents the number --> `0` occurred `2` times in `nums` so at `index = 0` we will write `2`.
- We then loop over our original `nums` array and replace the original array with the numbers in order of index and occurrence from `counts` array.
- For example, whilst overwriting the `nums` array we will loop over `counts` index `0` **two** times and each iteration we will write `0` in `nums` array twice in order --> `nums = [0, 0, ...]`.

## Code Implementation

### Solution - Bucket Sort

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        # We will use bucket sort (counting sort).
        unique_nums = len(set(nums))
        if unique_nums == 1:
            return

        counts = [0] * (max(nums) + 1)

        # Increment the counts (number of times a colour appeared).
        for i in range(len(nums)):
            counts[nums[i]] += 1

        n = 0
        for i in range(len(counts)):
            for j in range(counts[i]):
                nums[n] = i
                n += 1
```
