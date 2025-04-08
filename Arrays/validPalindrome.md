# Valid Palindrome (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**125. Valid Palindrome**](https://leetcode.com/problems/valid-palindrome/)

---

## Problem Statement

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

---

## Example 1

**Input:**

```python
s = "A man, a plan, a canal: Panama"
```

**Output:**

```python
true
```

**Explanation:**

```plaintext
After removing non-alphanumeric characters and converting to lowercase:
"amanaplanacanalpanama" → same forwards and backwards.
```

## Example 2

**Input:**

```python
s = "race a car"
```

**Output:**

```python
false
```

**Explanation:**

```plaintext
After cleaning: "raceacar" → not a palindrome.
```

## Example 3

**Input:**

```python
s = " "
```

**Output:**

```python
true
```

**Explanation:**

```plaintext
After removing non-alphanumeric characters, the string becomes "".
An empty string is a valid palindrome by definition.
```

---

## Constraints:

- `1 <= s.length <= 2 * 10⁵`
- `s consists only of printable ASCII characters`

---

## Approach & Algorithm

- I've utilised a two pointer approach to solve this problem.
- We must first and foremost remove any and all non-alphanumeric characters and ensure the remaining characters in the string are all lowercase.
- After that we can begin with the two pointer appraoch whereby we have pointers `L` and `R` that point to the leftmost and rightmost values in the string respectively.
- We compare the values respectively at each index to the opposite corresponding index value. The movement of pointers happens in unison and harmony whereby we always increment and decrement values by `1`.
- However, if we find an instance where the left and right pointers point to inherently different characters we know that the string is **NOT** a palindrome and hence we must return `False` immediately. Otherwise, upon the completion of the loop we know that the string is a valid palindrome and as such we must return `True`.

## Code Implementation:

### Solution One:

- **Time Complexity:** `O(n)`

```python
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        # We must remove all non-alphanumeric characters and make everything lowercase.
        updatedStr = re.sub(r'[^a-zA-Z0-9]', '', s).lower()

        L, R = 0, len(updatedStr) - 1

        while L < R:
            if updatedStr[L] != updatedStr[R]:
                # Characters don't match we must return 'False'.
                return False

            # Otherwise we must shift our pointers and compare next characters.
            L += 1
            R -= 1

        return True
```
