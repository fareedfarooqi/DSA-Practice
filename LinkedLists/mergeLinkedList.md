# Merge Two Sorted Lists (Easy)

## Problem Description

You are given the heads of two sorted linked lists, `list1` and `list2`.

Merge the two lists into one sorted linked list. The merged list should be created by **splicing together the nodes** of the first two lists.

Return the **head of the merged linked list**.

---

## Examples

### Example 1:

**Input**  
`list1 = [1,2,4]`  
`list2 = [1,3,4]`

**Output**  
`[1,1,2,3,4,4]`

---

### Example 2:

**Input**  
`list1 = []`  
`list2 = []`

**Output**  
`[]`

---

### Example 3:

**Input**  
`list1 = []`  
`list2 = [0]`

**Output**  
`[0]`

---

## Constraints

1. The number of nodes in both lists is in the range `[0, 50]`.
2. `-100 <= Node.val <= 100`
3. Both `list1` and `list2` are **sorted in non-decreasing order**.

---

## Approach & Algorithm

We will use a **dummy node approach** to merge the two sorted linked lists efficiently:

### Steps:

1. **Create a Dummy Node**:

   - Use a dummy node to simplify the process of merging the lists.
   - Maintain a `tail` pointer to track the last node in the merged list.

2. **Traverse Both Lists**:

   - Compare the `val` attributes of the current nodes of `list1` and `list2`.
   - Append the smaller node to the merged list, and move the respective pointer (`list1` or `list2`) forward.

3. **Attach Remaining Nodes**:

   - Once one list is fully traversed, attach the remaining nodes of the other list to the merged list.

4. **Return the Merged List**:
   - The merged list starts from `dummy.next`. Remember that the `dummy` node is simply a placeholder to allow us to simplify operations.

---

## Code Implementation

### Python Implementation

- **Time Complexity:** O(n + m) --> We need to traverse two linked lists.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        # Create a dummy node
        dummy = ListNode(-1)
        tail = dummy

        # Traverse both lists and merge
        while list1 is not None and list2 is not None:
            if list1.val <= list2.val:
                tail.next = list1
                list1 = list1.next
            else:
                tail.next = list2
                list2 = list2.next
            tail = tail.next

        # Attach remaining nodes, if any
        if list1 is not None:
            tail.next = list1
        elif list2 is not None:
            tail.next = list2

        # Return the merged list starting from dummy.next
        return dummy.next
```
