# Implement Stack using Queues (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Implement Stack using Queues**](https://leetcode.com/problems/implement-stack-using-queues/description/)

---

## Problem Description

Implement a last-in-first-out (LIFO) **stack** using only two **queues**. The implemented stack should support all the standard functions of a normal stack:

- `push(int x)`: Pushes element `x` to the top of the stack.
- `pop()`: Removes the element on the top of the stack and returns it.
- `top()`: Returns the element on the top of the stack.
- `empty()`: Returns `true` if the stack is empty, `false` otherwise.

### Notes:

- You must use only the standard operations of a queue:
  - Push to back (`enqueue`).
  - Peek/pop from front (`dequeue`).
  - Check size.
  - Check if empty.
- Depending on the language, the queue may not be natively supported. You may simulate a queue using a list or deque (double-ended queue) as long as you use only the queue's standard operations.

---

## Examples

### Example 1:

**Input**:

`["MyStack", "push", "push", "top", "pop", "empty"]`
`[[], [1], [2], [], [], []]`

**Output**:
`[null, null, null, 2, 2, false]`

**Explanation**:

- MyStack myStack = new MyStack();
- myStack.push(1); // Push 1 onto the stack
- myStack.push(2); // Push 2 onto the stack
- myStack.top(); // Return 2 (top of the stack)
- myStack.pop(); // Return 2 and remove it from the stack
- myStack.empty(); // Return False (stack is not empty)

## Approach & Algorithm

We will use **two queues** to solve this problem.

### Steps:

- So, our `queueOne` variable is our main queue that will store the values in the appropriate **LIFO** order as required.
- `queueTwo` is used as a temporary array whereby when we push a number into our stack, the `queueTwo` is first cleared and numbers are then copied into `queueTwo` from `queueOne`.
- After the copying of numbers, we append the new `val` into `queueOne` (meaning `queueOne` only has a length of 1 at this time).
- After this we concatenate elements from `queueTwo` into `queueOne`. `queueOne` will have a length of `queueOne` + `queueTwo`.
- `pop()`, `top()`, `empty()` have self-explanatory logic.

---

## Code Implementation

### Python Implementation

- **Time Complexity:** O(1) --> For all methods.

```python
class MyStack:

    def __init__(self):
        self.queueOne = []
        self.queueTwo = []

    def push(self, x: int) -> None:
        if len(self.queueOne) == 0:
            self.queueOne.append(x)
            return

        # Otherwise we need to copy over to queueTwo temporarily.
        self.queueTwo.clear()
        self.queueTwo = self.queueOne[:]
        self.queueOne.clear()
        self.queueOne.append(x)
        self.queueOne = self.queueOne + self.queueTwo

    def pop(self) -> int:
        return self.queueOne.pop(0)

    def top(self) -> int:
        return self.queueOne[0]

    def empty(self) -> bool:
        return True if len(self.queueOne) == 0 else False


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```
