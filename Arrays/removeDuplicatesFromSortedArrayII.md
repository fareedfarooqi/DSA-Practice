# Remove Duplicates from Sorted Array II (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**80. Remove Duplicates from Sorted Array II**](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

---

## **Problem Statement**

Given an integer array `nums` sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` after placing the final result in the first `k` slots of `nums`.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with **O(1)** extra memory.

---

## **Custom Judge**

The judge will test your solution with the following code:

```cpp
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be accepted.

---

## **Example 1**

**Input:**
```python
nums = [1,1,1,2,2,3]
```

**Output:**
```python
5, nums = [1,1,2,2,3,_]
```

**Explanation:**
Your function should return k = 5, with the first five elements of nums being 1, 1, 2, 2, 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

## **Example 2**

**Input:**
```python
nums = [0,0,1,1,1,1,2,3,3]
```

**Output:**
```python
7, nums = [0,0,1,1,2,3,3,_,_]
```

**Explanation:**
Your function should return k = 7, with the first seven elements of nums being 0, 0, 1, 1, 2, 3, 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

## Constraints

- `1 <= nums.length <= 3 * 10⁴`
- `10⁴ <= nums[i] <= 10⁴`
- `nums` is sorted in non-decreasing order.

---

## Approach & Algorithm:

- Solution One is significantly faster and teh optimal approach to solving this question. We use some form of a two-pointer approach in a one-pass manner to solve this question.
- In particular, we loop over the `nums` array and we check for the conditions:
  - Whether `i` (like a writing pointer - helps us track at what index we will next write in the array) is less than `2`. This is crucial as at most we can have two duplicates. But it mostly is used for the first part of the algorithm to get it started. Without it the next condition would not be possible to check as we would be going out of bounds.
  - We otherwise check if the `num` we are currently looping over has been seen 2 indexes before i.e., `nums[i - 2]`.
- If either of those conditions above pass we have found a new number or a first time duplicate. As such we place this `num` in the index that `i` points to.
- We can then return `i` as it keeps track of the last index we overwrote/wrote at.

## Code Implementation

### Solution One (Faster):

- **Time Complexity:** O(n)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0

        for num in nums:
            if i < 2 or num != nums[i - 2]:
                # We have found a new number OR first time duplicate.
                nums[i] = num
                i += 1
        
        return i
```

### Solution Two (Slow - NOT Optimal):

- **Time Complexity:** O(n^2)
- **NOTE:** This is a hacky solution. We are not following the specs requirements appropriately. There is also a hardcoded `100000000` that is placed in the solution. This could fail test cases involving that number etc.

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        duplicateCount = 0

        for L in range(len(nums)):
            duplicateFound = False
            for R in range(L + 1, len(nums)):
                if nums[L] != nums[R]:
                    break

                if nums[L] == nums[R] and not duplicateFound:
                    # We have not found a previous duplicate.
                    # This is the first time we have spotted a duplicate.
                    duplicateFound = True
                elif nums[L] == nums[R] and duplicateFound:
                    # We found another duplicate. This is not good as we have already found a duplicate before.
                    nums[L] = 100000000
                    duplicateCount += 1

            duplicateFound = False
       
        nums.sort()
        
        return len(nums) - duplicateCount
```