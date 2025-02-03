# Sort an Array (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Sort an Array**](https://leetcode.com/problems/sort-an-array/description/)

---

## **Problem Statement**

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in functions** in **O(n log n)** time complexity and with the **smallest space complexity possible**.

---

## **Example 1**

**Input**:

```python
nums = [5,2,3,1]
```

**Output**:

```python
[1,2,3,5]
```

## **Explanation**

After sorting the array, the positions of some numbers are unchanged (e.g., `2` and `3`), while others have changed (e.g., `1` and `5`).

---

## **Example 2**

**Input**:

```python
nums = [5,1,1,2,0,0]
```

**Output**:

```python
[0,0,1,1,2,5]
```

## **Explanation**

The values of `nums` are not necessarily unique.

---

## **Constraints**

- `1 <= nums.length <= 5 * 10⁴`
- `-5 * 10⁴ <= nums[i] <= 5 * 10⁴`

---

## Approach & Algorithm

- I initally used a regular `quickSort` algorithm to solve this question. I passed most cases, however I would get a `Time Limit Exceeded` error with solutions `1` and `2`. The reason being because both these approaches had a worst-case time-complexity of `O(n^2)`. This is even more evident when the nums array have many duplicates such as `[2, 2, 2, ..., 2]` or [3, 2, 2, 2, ..., 2]. Solution `2` was a bit faster because I put the `nums` array into a set and checked if there was only 1 element, if so I simply returned the `nums` array as it would automatically be sorted.
- However, solutions `1` and `2`, did not yield a result which had me pass all the test cases.
- This is where I utilised the `Three-Way Partitioning (Dutch National Flag Algorithm)`. It involved me breaking the `nums` array into 3 partitioned sections where, we choose a pivot whereby there are numbers to the left of the pivot which are **smaller**, numbers infront of the pivot which are **greater**, and numbers next to it in place where numbers are **equal** to the pivot (handles duplicates). I had 3 pointers, `low`, `mid` and a `high` pointer.
- `low` pointer keeps track of where small elements (**less** than pivot) should go.
- `mid` pointer scans each number during our pass.
- `high` pointer keeps track of where big elements (**greater** than pivot) should go.

### Three-Way Partitioning (Dutch National Flag Algorithm) Logic

![IMG_3238](https://github.com/user-attachments/assets/aa038fd2-0211-46f7-8749-0b2638192644)
![IMG_3239](https://github.com/user-attachments/assets/13d0af19-6ad3-489a-8264-189cbe20394c)
![IMG_3240](https://github.com/user-attachments/assets/1d6c8d65-d6fa-4071-9e06-bb504e70356e)
![IMG_3241](https://github.com/user-attachments/assets/3d33981e-52be-4868-93c7-449d65a5a6fd)
![IMG_3242](https://github.com/user-attachments/assets/51c9adef-7001-42db-a244-fb0527c66c94)

## Code Implementation

### Solution 1 (Slowest - Not Optimised)

- **Time Complexity:** O(n^2)

```python
class Solution:
def sortArray(self, nums: List[int]) -> List[int]:
return self.quickSort(nums, 0, len(nums) - 1)

    def quickSort(self, nums, start, end):
        # Base Case: Check if length of interpreted nums is <= 1
        if (end - start + 1) <= 1:
            return nums

        pivot = nums[end]
        left_ptr = start
        print(f"{pivot} and {nums[left_ptr]}")

        for i in range(start, end):
            if nums[i] <= pivot:
                # Perform the swap
                nums[left_ptr], nums[i] = nums[i], nums[left_ptr]
                left_ptr += 1

        # Swap pivot value with where left_ptr points
        nums[left_ptr], nums[end] = nums[end], nums[left_ptr]

        # Sort recursively
        self.quickSort(nums, start, left_ptr - 1)
        self.quickSort(nums, left_ptr + 1, end)

        return nums
```

### Solution 2 (Slower than Solution 3 but faster than Solution 2 - Somewhat Optimised)

- **Time Complexity:** O(n^2)

```python
class Solution:
def sortArray(self, nums: List[int]) -> List[int]:
if len(set(nums)) == 1:
return nums

        return self.quickSort(nums, 0, len(nums) - 1)

    def quickSort(self, nums, start, end):
        # Base Case: Check if length of interpreted nums is <= 1
        if end <= start:
            return nums

        # To optimise the algorithm we can use a random pivot value
        pivot_index = random.randint(start, end)
        nums[pivot_index], nums[end] = nums[end], nums[pivot_index]

        pivot = nums[end]
        left_ptr = start

        for i in range(start, end):
            if nums[i] <= pivot:
                # Perform the swap
                nums[left_ptr], nums[i] = nums[i], nums[left_ptr]
                left_ptr += 1

        # Swap pivot value with where left_ptr points
        nums[left_ptr], nums[end] = nums[end], nums[left_ptr]

        # Sort recursively
        self.quickSort(nums, start, left_ptr - 1)
        self.quickSort(nums, left_ptr + 1, end)

        return nums
```

### Solution 3 (Fastest - Passes ALL Test Cases)

- **Time Complexity:** O(n\*log(n))

```python
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        return self.quickSort(nums, 0, len(nums) - 1)

    def quickSort(self, nums, start, end):
        # Base Case: Check if length of interpreted nums is <= 1
        if end <= start:
            return nums

        # To optimise the algorithm we can use a random pivot value
        pivot_index = random.randint(start, end)
        pivot = nums[pivot_index]

        low, mid, high = start, start, end

        while mid <= high:
            if nums[mid] < pivot:
                nums[mid], nums[low] = nums[low], nums[mid]
                low += 1
                mid += 1
            elif nums[mid] > pivot:
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
            else:
                mid += 1

        self.quickSort(nums, start, low - 1)
        self.quickSort(nums, high + 1, end)

        return nums
```
