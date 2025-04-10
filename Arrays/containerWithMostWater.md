# Container With Most Water (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**11. Container With Most Water**](https://leetcode.com/problems/container-with-most-water/)

---

## **Problem Statement**

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`th line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

**Notice:** You may not slant the container.

---

## **Example 1**

![1](https://github.com/user-attachments/assets/72b75bc3-3c86-4f63-a527-0178f54fda04)


**Input:**
```python
height = [1,8,6,2,5,4,8,3,7]
```

**Output:**
```python
height = [1,1]
```

**Explanation:**
The above vertical lines are represented by array `[1,8,6,2,5,4,8,3,7]`.
In this case, the max area of water (blue section) the container can contain is `49`.

## **Example 2**

**Input:**
```python
height = [1,1]
```

**Output:**
```python
1
```

## Constraints

- `n == height.length`
- `2 <= n <= 10⁵`
- `0 <= height[i] <= 10⁴`

---

## Approach & Algorithm

- Initially, I came up with a brute force solution to this problem as per my solution two below. However, it was simply too slow.
- I then came up with another approach as per solution one. If we pay close attention to the examples provided in the specification we can observe that a two-pointer approach is possible. I have two left and right pointers `L` and `R` respectively. I keep looping until these pointers overlap at which point we stop our loop.
- The main idea is we work outward-in. So we begin by finding the area of the outermost lines. We see if this area we calculated is greater than the `maxArea` we have stored. If it is we replace it.
- The key to solving this question is to move the pointers appropriately. We shift the `L` pointer up by one if the value that `L` points to is smaller than the value that `R` points to, i.e., `height[L] < height[R]`. The opposite case would require us to shift the `R` pointer down by one.
- Utilising this approach we can in essence find the max area in one-pass.

## Code Implementation:

### Solution One (Fastest):

- **Time Complexity:** O(n)

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        L, R = 0, len(height) - 1
        maxArea = 0

        while L < R:
            minHeight = min(height[L], height[R])
            width = R - L
            curArea = minHeight * width

            if curArea > maxArea:
                maxArea = curArea

            # We check to see which line is longer. We move in from the side where the line is shorter.
            if height[L] < height[R]:
                L += 1
            else:
                R -= 1
        
        return maxArea
```

### Solution One (SLOW - TLE):

- **Time Complexity:** O(n^2)

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        curArea = 0
        maxArea = 0

        for L in range(len(height)):
            for R in range(L + 1, len(height)):
                # We must find the min() between the two heights in the array.
                minHeight = min(height[R], height[L])
                width = R - L
                curArea = minHeight * width
                
                if curArea > maxArea:
                    maxArea = curArea

        return maxArea
```
