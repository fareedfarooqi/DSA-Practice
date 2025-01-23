# Valid Parentheses

## Problem Description

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid.

An input string is **valid** if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every closing bracket has a corresponding opening bracket of the same type.

---

## Examples

### **Example 1**

**Input:**  
`s = "()"`  
**Output:**  
`true`

---

### **Example 2**

**Input:**  
`s = "()[]{}"`  
**Output:**  
`true`

---

### **Example 3**

**Input:**  
`s = "(]"`  
**Output:**  
`false`

---

### **Example 4**

**Input:**  
`s = "([])"`  
**Output:**  
`true`

---

## Constraints

- `1 <= s.length <= 10⁴`
- `s` consists only of parentheses characters: `'()[]{}'`.

---

## Approach & Algorithm

### 1. Stack-Based Solution

This problem can be efficiently solved using a stack and a dictionary. The idea is:

1. Use a stack to keep track of unmatched **opening brackets**. We also having a mapping dictionary to show mapping of each closing bracket to it's corresponding bracket.
2. Iterate through each character in the string `s`:
   - If the character is an **opening bracket** as per the mapping (it is in `mapping.values()`), push it onto the stack.
   - If the character is a **closing bracket** as per the mapping (it is in `mapping.keys()`), check:
     - If the stack is empty, it means there is no corresponding opening bracket (return `false`).
     - Otherwise, pop the top element from the stack and verify that it matches the closing bracket using the mapping.
3. After processing all characters, check if the stack is empty:
   - If it is empty, all brackets are matched (return `true`).
   - If not, some opening brackets are unmatched (return `false`).

I have provided a written example in the image attached.

![IMG_3209](https://github.com/user-attachments/assets/a804dd8d-50a5-433a-ad13-cba82f7f5090)

## Code Implementation

- **Time Complexity:** O(n)

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        mapping = {")": "(", "}": "{", "]": "["}

        for char in s:
            if char in mapping.values():
                stack.append(char)
            elif char in mapping.keys():
                if not stack or mapping[char] != stack.pop():
                    return False

        return not stack
```
