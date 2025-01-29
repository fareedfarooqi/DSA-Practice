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

### Solution One: Iterative

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

### Solution Two: Recursive

1. We check to see if the list is empty, if it is we return `None`.
2. We keep recursing down the list i.e., if we have `list = [1, 2, 3, 4, 5]`, we are traversing down to node `5` as long as `head.next` is not `None` (NULL).
3. Once we are at the final node i.e.,`5` in our example, we know that the `head.next` is **indeed** `None` now. So we skip recursing further and set the `head` node, `5` in our example to point to `None` (NULL). We then return our `newHead` which is `5` in our example now.
4. We are then at node `4`, `[ 1 -> 2 -> 3 -> 4 ]` and `[ 5 -> None ]`. Note that `5` was returned as our `newHead` from the line `newHead = self.reverseList(head.next)`. Our `head` is `4`. We continue to the next line, which is `head.next.next = head`. This is essentially swapping where our pointer points. So `head.next.next` is saying in our example `5.next = 4`, meaning node `5` now points to node `4`.
5. We keep repeating this process until all nodes are reversed.

---

## Code Implementation

### Solution One: Iterative

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

### Solution Two: Recursive

- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # Recursive Solution

        # If list is empty return None
        if not head:
            return None

        newHead = head
        if head.next:
            newHead = self.reverseList(head.next)
            # Basically below line is saying to change where the pointer points
            # [ 2 -> 3 ] ====> [2 <- 3 ]
            head.next.next = head
        head.next = None

        return newHead
```
