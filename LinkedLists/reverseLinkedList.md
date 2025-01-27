# Reverse Linked List (Easy)

## Problem Description

Given the head of a singly linked list, reverse the list, and return the reversed list.

---

## Examples

### Example 1:

**Input**  
`head = [1,2,3,4,5]`

**Output**  
`[5,4,3,2,1]`

---

### Example 2:

**Input**  
`head = [1,2]`

**Output**  
`[2,1]`

---

### Example 3:

**Input**  
`head = []`

**Output**  
`[]`

---

## Constraints

- The number of nodes in the list is in the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

---

## Approach & Algorithm

To reverse a singly linked list, we use the **three-pointer approach**. These pointers are:

1. **`prev`**: Tracks the previous node (initially set to `None`).
2. **`cur`**: Tracks the current node (initially set to the `None`').
3. **`next`**: Temporarily stores the next node to maintain the traversal while reversing links. Initially we set it to `head`.

### Steps:

1. Initialize `prev = None` and `cur = None`.
2. Iterate through the list until `next` becomes `None`:
   - Move `cur` forward to `next`.
   - Store the next node in `next` (`next = next.next`). So we just set the next node to whatever node the it's address it was pointing too.
   - Reverse the `next` pointer of `cur` (`cur.next = prev`).
   - Move `prev` forward to `cur` (`prev = cur`).
3. At the end of the loop, `cur` will point to the new head of the reversed list.
4. Return `cur`.

---

## Code Implementation

- **Time Complexity:** O(n)

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Check if the list is empty
        if not head:
            return None

        # We will use 3 pointers.
        prev = None
        cur = None
        next = head

        # Our cur and prev pointers are always a step behind.
        while next is not None:
            cur = next
            next = next.next
            cur.next = prev
            prev = cur

        return cur
```
