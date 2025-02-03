# Search a 2D Matrix (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Search a 2D Matrix**](https://leetcode.com/problems/search-a-2d-matrix/)

---

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` is in `matrix` or `false` otherwise.

You must write a solution in **O(log(m \* n))** time complexity.

## Example 1:

**Input:**

```python
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
```

**Output:**

```python
true
```

## Example 2:

**Input:**

```python
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
```

**Output:**

```python
false
```

---

## Approach & Algorithm

- The key to understanding this problem was observing that it requires **two** binary searches to be performed.
- My intuition was that I should first start with a `row` binary search whereby I attempt to locate where the `row` containing the `target` could be.
- Whilst performing the binary search for the row, I would check whether the `target > matrix[midRow][rightColPtr]` meaning that the target was greater than the last value in the row we are performing the binary search on. This means that the row we are searching is **incorrect** and as such the correct row must be to the right of the current **midRow**. I would also check whether `target < matrix[midRow][leftColPtr]` meaning that the target was smaller than the first value in the row we are performing the binary search on. This means that the row we are searching is **incorrect** and as such the correct row must be to the left of the current **midRow**. Otherwise we are in the correct row and can continue.
- If we are in the correct row we search for the **target** using the binary search algorithm on a normal array.

---

## Code Implementation

### Python Implementation

- **Time Complexity**: O(log(m \* n)) OR O(log(m)) + O(log(n))

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        leftRowPtr, rightRowPtr = 0, len(matrix) - 1
        midRow = 0

        while leftRowPtr <= rightRowPtr:
            midRow = (leftRowPtr +rightRowPtr) // 2
            leftColPtr, rightColPtr = 0, len(matrix[midRow]) - 1
            midCol = 0

            if target > matrix[midRow][rightColPtr]:
                leftRowPtr = midRow + 1
                continue
            elif target < matrix[midRow][leftColPtr]:
                rightRowPtr = midRow - 1
                continue

            # Otherwise we know it's in this row

            while leftColPtr <= rightColPtr:
                midCol = (leftColPtr + rightColPtr) // 2
                if target > matrix[midRow][midCol]:
                    leftColPtr = midCol + 1
                elif target < matrix[midRow][midCol]:
                    rightColPtr = midCol - 1
                else:
                    return True

            return False

        return False
```
