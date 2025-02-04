# Koko Eating Bananas (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Koko Eating Bananas**](https://leetcode.com/problems/koko-eating-bananas/)

---

## Problem Description

Koko loves to eat bananas. There are `n` piles of bananas, where the `i-th` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed `k`. Each hour, she **chooses one pile** of bananas and eats `k` bananas from that pile. If the pile has **less than `k` bananas**, she eats all of them and **will not eat any more bananas during this hour**.

Koko **likes to eat slowly** but still wants to **finish eating all the bananas before the guards return**.

Return the **minimum integer `k`** such that she can eat all the bananas **within `h` hours**.

---

## Examples

### **Example 1**

**Input:**

```python
piles = [3,6,7,11], h = 8
```

**Output:**

```python
4
```

### **Example 2**

**Input:**

```python
piles = [30,11,23,4,20], h = 5
```

**Output:**

```python
30
```

### **Example 3**

**Input:**

```python
piles = [30,11,23,4,20], h = 6
```

**Output:**

```python
23
```

---

## Approach & Algorithm

- The trick to this question is understanding that we need to find a `k` such that it is the **minimum** (`k` represents number of bananas) that Koko can eat in an hour such that he can finish all the bananas in all of the piles.
- So we start off by initially setting `leftPtr = 1`, because that is truly the minimum positive number of bananas that Koko can eat in an hour such that he is able to eat all bananas from all of the piles.
- We set `rightPtr = max(piles)` because we need to find the upper limit on the number of bananas Koko can eat in an hour.
- We loop until `leftPtr == rightPtr` at which point we know we have found a minimum `k` whereby `k == leftPtr`.
- During the loop we adjust our `mid` pointer to find the middle value in the range `[leftPtr, ..., rightPtr]`.
  - We then find a value of `k` by summing the number of bananas that can be eaten by Koko from each pile given that he can only eat at most `mid` number of bananas in **one** hour.
  - If `k < h` then we know that Koko cannot eat all the bananas before the guards return (meaning he is too slow and `k` needs to increase). So we adjust our `leftPtr`.
  - Otherwise we know that we have found a `k` such that Koko is able to finish eating all bananas in all of the piles **before** the guards get back. But we keep looping to ensure that there may be no remaining values that are less than `k` that satisfy the prerequisite of Koko finishing eating all of the bananas in all of the piles before the guards return.

## Code Solutions

- **Time Complexity**: It is `O(n * log(piles))`.

```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        leftPtr, rightPtr = 1, max(piles)

        while leftPtr < rightPtr:
            mid = (leftPtr + rightPtr) // 2
            k = sum(math.ceil(pile / mid) for pile in piles)

            if k > h:
                # Too Slow
                leftPtr = mid + 1
            else:
                rightPtr = mid

        return leftPtr
```
