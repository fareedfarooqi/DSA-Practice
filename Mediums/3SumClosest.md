# 3Sum Closest (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**16. 3Sum Closest**](https://leetcode.com/problems/3sum-closest/)

---

## **Problem Statement**

Given an integer array `nums` of length `n` and an integer `target`, find **three integers** in `nums` such that their sum is **closest** to `target`.

Return the **sum of the three integers**.

You may assume that **each input would have exactly one solution**.

---

## **Example 1**

**Input:**
```python
nums = [-1,2,1,-4]
target = 1
```

**Output:**
```python
2
```

**Explanation:**
The sum that is closest to the target is `2` `(-1 + 2 + 1 = 2)`.

## **Example 2**

**Input:**
```python
nums = [0,0,0]
target = 1
```

**Output:**
```python
0
```

**Explanation:**
The sum that is closest to the target is `0` `(0 + 0 + 0 = 0)`.

## Constraints

- `3 <= nums.length <= 500`
- `1000 <= nums[i] <= 1000`
- `10⁴ <= target <= 10⁴`

---

## Approach & Algorithm

- I've utilised a two-pointer approach with a bit of a twist to solve this question.
- The trick to understanding this question is that we can 'fix' the position of one number i.e., `i` in our solution one below and then we can use a two pointer approach to find which number is closest to the `target` (we call that `closestSum`) and return that number.
- I also sort the `nums` array to better allow us to use the two pointer approach with better time complexity. So for the two pointer approach, I have a `leftPtr` and a `rightPtr` which are initially set to the first number after `i` (`i + 1`) and `n - 1` (the last valid array element). I then compute the sum of the corresponding numbers `sumInIter = nums[i] + nums[leftPtr] + nums[rightPtr]` and see if this yields a number that is closer to `target` than our previous `closestSum` in our last iteration. If during our iteration the `sumInIter` is smaller or larger than our `target` we adjust our `leftPtr` and `rightPtr` respectively.

## Code Implementation

### Solution One:

- **Time Complexity:** O(n^2)
- **Space Complexity:** O(1)

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        closestSum = float('inf')
        nums.sort()
        n = len(nums)
        
        # We want there to always be three numbers so we can add them properly.
        for i in range(n - 2):
            leftPtr, rightPtr = i + 1, n - 1

            # We are using two pointer approach now.
            while leftPtr < rightPtr:
                sumInIter = nums[i] + nums[leftPtr] + nums[rightPtr]
                
                if abs(sumInIter - target) < abs(closestSum - target):
                    closestSum = sumInIter

                if sumInIter < target:
                    # Meaning we are still smaller than target, we must increment.
                    leftPtr += 1
                elif sumInIter > target:
                    # We have overshot and are greater than target, we must decrement.
                    rightPtr -= 1
                else:
                    # We have found the exact sum.
                    return sumInIter
        
        return closestSum
```

### Solution Two (TLE - TOO SLOW):

- **Time Complexity:** O(n^3)
- **Space Complexity:** O(1)

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        total = float('inf')
        nums.sort()
        for i in range(len(nums)):
            for j in range(i + 1, len(nums), 1):
                for k in range(len(nums) - 1, j, -1):
                    totalInIter = nums[i] + nums[j] + nums[k]
                    if abs(totalInIter - target) < abs(total - target):
                        total = totalInIter
        return total
```