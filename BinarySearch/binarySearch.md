# Binary Search (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Binary Search**](https://leetcode.com/problems/binary-search/description/)

---

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with **O(log n)** runtime complexity.

## Example 1:

**Input:**  
`nums = [-1,0,3,5,9,12]`, `target = 9`  
**Output:**  
`4`  
**Explanation:**  
9 exists in `nums` and its index is `4`.

## Example 2:

**Input:**  
`nums = [-1,0,3,5,9,12]`, `target = 2`  
**Output:**  
`-1`  
**Explanation:**  
2 does not exist in `nums` so return `-1`.

## Constraints:

- `1 <= nums.length <= 10^4`
- `-10^4 < nums[i], target < 10^4`
- All the integers in `nums` are unique.
- `nums` is sorted in ascending order.

---

## Approach & Algorithm

- This question required that I utilise the well known **binary search** algorithm.
- I utilised two pointers, `leftPtr` and `rightPtr` which kept track of the boundaries of the search itself (between what indexes should we be searching).
- I had a variable called `mid` which kept track of the middle value in the input.
- We then looped until `leftPtr` became greater than `rightPtr` (meaning our left most index is now greater than rightmost index --> this doesn't make much sense as the `rightPtr` was intially set to the last most value in the input. When `leftPtr` overlaps and goes over the `rightPtr` one of two things have happened. We are either beyond the length of the array with our `leftPtr` **or** we are searching for values that have already been eliminated - did not pass the search).
- If the value of `target > nums[mid]` then we know that our target lies toward the right side of our current `mid` so we adjust our `leftPtr`.
- If the value of `target < nums[mid]` then we know that our target lies toward the left side of our current `mid` so we adjust our `rightPtr`.
- Otherwise we have found our value and we return `mid`.

---

## Code Implementation

### Python Implementation

- **Time Complexity**: O(log(n))

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        leftPtr, rightPtr = 0, len(nums) - 1
        mid = -1

        while leftPtr <= rightPtr:
            mid = (leftPtr + rightPtr) // 2

            if target > nums[mid]:
                leftPtr = mid + 1
            elif target < nums[mid]:
                rightPtr = mid - 1
            else:
                return mid

        return -1
```
