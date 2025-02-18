# Single Number (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Single Number**](https://leetcode.com/problems/single-number/)

---

## Problem Statement

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a **linear runtime complexity** and use only **constant extra space**.

---

## **Example 1**

**Input:**

```python
nums = [2,2,1]
```

**Output:**

```python
1
```

## **Example 2**

**Input:**

```python
nums = [4,1,2,1,2]
```

**Output:**

```python
4
```

## **Example 3**

**Input:**

```python
nums = [1]
```

**Output:**

```python
1
```

## Constraints

- `1 <= nums.length <= 3 * 10⁴`
- `3 * 10⁴ <= nums[i] <= 3 * 10⁴`
- `Each element in the array appears twice except for one element, which appears only once.`

---

## Approach & Algorithm

- The trick to this question is recognizing it is a **bit manipulation problem**, specifically leveraging the **XOR operator**.
- The **XOR (^) properties** we use:
  - `x XOR x = 0` (Same numbers cancel out)
  - `x XOR 0 = x` (XOR with 0 does NOT change the number)
- Since every number appears **twice** except for **one unique number**, XORing **all numbers together** will cancel out the duplicates, leaving only the single number.

### **Example Walkthrough (`nums = [2, 2, 1]`)**

1. **Initialize `result = 0`**
2. **First iteration (`num = 2`)**:
   - `result = 0 XOR 2 = 2`
3. **Second iteration (`num = 2`)**:
   - `result = 2 XOR 2 = 0` (Since `x XOR x = 0`)
4. **Third iteration (`num = 1`)**:
   - `result = 0 XOR 1 = 1` (Since `x XOR 0 = x`)
5. **Final result = 1**, which is the single number in the array.

## Code Implementation

### Solution:

- **Time Complexity:** O(n).

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0

        for num in nums:
            result ^= num

        return result
```
