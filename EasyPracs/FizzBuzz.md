# Fizz Buzz (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Fizz Buzz**](https://leetcode.com/problems/fizz-buzz/description/)

---

## Problem Description

Given an integer `n`, return a **string array** `answer` (1-indexed) where:

- `answer[i] == "FizzBuzz"` if `i` is **divisible by both 3 and 5**.
- `answer[i] == "Fizz"` if `i` is **divisible by 3**.
- `answer[i] == "Buzz"` if `i` is **divisible by 5**.
- `answer[i] == i` (as a string) **if none of the above conditions apply**.

The function should **generate results from `1` to `n`**.

---

## **Examples**

### **Example 1**

**Input**:

```python
n = 3
```

**Output**:

```python
["1", "2", "Fizz"]
```

### **Example 2**

**Input**:

```python
n = 5
```

**Output**:

```python
["1", "2", "Fizz", "4", "Buzz"]
```

### **Example 3**

**Input**:

```python
n = 15
```

**Output**:

```python
["1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8", "Fizz", "Buzz", "11", "Fizz", "13", "14", "FizzBuzz"]
```

## Constraints

- `1 <= n <= 10⁴`
- Generate results from `1` to `n`.

---

## Approach & Algorithm

- We utilize the **modulo operator (`%`)** to determine divisibility.
- We use Python's `range()` function to generate values from `[1, ..., n]`.
- The **modulo operator (`%`)** helps us check whether a number is **divisible** by 3, 5, or both:
  - If `i % 3 == 0 and i % 5 == 0`, append `"FizzBuzz"`.
  - If `i % 3 == 0`, append `"Fizz"`.
  - If `i % 5 == 0`, append `"Buzz"`.
  - Otherwise, append the **number as a string**.
- This ensures we generate the correct FizzBuzz sequence **efficiently**.

## Code Implementation

### Solution:

- **Time Complexity:** O(n)

```python
class Solution:
def fizzBuzz(self, n: int) -> List[str]:
results = []

        for i in range(1, n + 1):
            if i % 3 == 0 and i % 5 == 0:
                results.append("FizzBuzz")
            elif i % 3 == 0:
                results.append("Fizz")
            elif i % 5 == 0:
                results.append("Buzz")
            else:
                results.append(str(i))

        return results
```
