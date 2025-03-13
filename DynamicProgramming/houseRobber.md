# House Robber (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**198. House Robber**](https://leetcode.com/problems/house-robber/)

---

## **Problem Statement**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed inside.  

However, **adjacent houses have security systems connected**, and if you rob **two adjacent houses**, the alarm will go off.  

Given an integer array `nums` representing the amount of money in each house, return **the maximum amount of money you can rob tonight** without alerting the police.

---

## **Example 1**

**Input:**
```python
nums = [1,2,3,1]
```

**Output:**
```python
4
```

**Explanation:**
```plaintext
Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

## **Example 2**

**Input:**
```python
nums = [2,7,9,3,1]
```

**Output:**
```python
12
```

**Explanation:**
```plaintext
Rob house 1 (money = 2), rob house 3 (money = 9), and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
```

## Constraints

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

---

## Approach & Algorithm

- I've utilised dynamic programming to solve this question.
- The key idea here is we are managing `rob1` and `rob2` variables. Visualise it as the following: `[rob1, rob2, n, n + 1, n + 2]`.
  - We loop through the `nums` array. We need to maintain the two variables `rob1` and `rob2` which are essentially keeping track of the max amount of money we can get by robbing homes. We can either be at `rob1 + n` or `rob2`.
  - We need rearrange and reset the values of `rob1` and `rob2` as we loop through `nums`.
- An example is `[2, 1, 1, 2]` and `rob1, rob2 = 0, 0`:
  - **Iteration 1:** `max(2, 0) = 2` --> `rob1 = 0` and `rob2 = 2`. `nums = [2, 1, 1, 2]` and `n = 2`
  - **Iteration 2:** `max(1 + 0, 2) = 2` --> `rob1 = 2` and `rob2 = 2`. `nums = [1, 1, 2]` and `n = 1`
  - **Iteration 3:** `max(1 + 2, 2) = 3` --> `rob1 = 2` and `rob2 = 3`. `nums = [1, 2]` and `n = 1`
  - **Iteration 4:** `max(3, 2 + 2) = 4` --> `rob1 = 3` and `rob2 = 4`. `nums = [2]` and `n = 2`
  - So **Final Output** is 4.

## Code Implementation

### Solution:

- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        rob1, rob2 = 0, 0

        for n in nums:
            temp = max(n + rob1, rob2)
            rob1 = rob2
            rob2 = temp
            
        return rob2
```


