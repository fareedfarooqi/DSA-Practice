# Min Stack

## Problem Description

Design a stack that supports the following operations in **constant time** (`O(1)`):

1. **`push(val)`**: Pushes the element `val` onto the stack.
2. **`pop()`**: Removes the element on the top of the stack.
3. **`top()`**: Retrieves the top element of the stack.
4. **`getMin()`**: Retrieves the minimum element in the stack.

You must implement the `MinStack` class with the above operations.

---

### Example 1:

**Input**
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

**Output**
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top(); // return 0
minStack.getMin(); // return -2

---

## Approach & Algorithm

### Two-Stack Approach

To implement a stack that supports `push`, `pop`, `top`, and `getMin` operations in **O(1)** time, we can use the **two-stack approach**. Here's how it works:

1. **Main Stack (`stack`)**:

   - This stack holds all the elements of the stack.

2. **Min Stack (`min_vals_stack`)**:
   - This stack tracks the minimum value at every point in the stack.
   - The top of this stack always holds the current minimum value of the main stack.

### Algorithm

1. **Initialization (`__init__`)**:

   - Create two stacks: `stack` and `min_vals_stack`.

2. **Push Operation (`push(val)`)**:

   - Push the element `val` onto the `stack`.
   - If `min_vals_stack` is empty or `val` is smaller than or equal to the current minimum (`min_vals_stack[-1]`), push `val` onto `min_vals_stack`.

3. **Pop Operation (`pop()`)**:

   - Remove the top element from the `stack`.
   - If the removed element is the same as the current minimum (`min_vals_stack[-1]`), also remove it from `min_vals_stack`.

4. **Top Operation (`top()`)**:

   - Return the top element of the `stack` (i.e., `stack[-1]`).

5. **Get Minimum Operation (`getMin()`)**:
   - Return the top element of `min_vals_stack` (i.e., `min_vals_stack[-1]`), which always holds the current minimum value of the `stack`.

### Key Points

- The `min_vals_stack` ensures that the minimum value is tracked in constant time.
- Each operation (`push`, `pop`, `top`, `getMin`) has a time complexity of **O(1)**.
- Space complexity is **O(n)** because both `stack` and `min_vals_stack` can store up to `n` elements.

---

## Code Implementation

- **Time Complexity:** O(1)

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_vals_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)

        if not self.min_vals_stack or val <= self.min_vals_stack[-1]:
            # Append the new smallest value to our second stack
            self.min_vals_stack.append(val)

    def pop(self) -> None:
        # If the number we are popping is the same as the current minimum number
        # (as per the second stack) we must set a new minimum value by popping from our second stack
        if self.top() == self.min_vals_stack[-1]:
            self.min_vals_stack.pop()

        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        if not self.min_vals_stack:
            return
        return self.min_vals_stack[-1]
```
