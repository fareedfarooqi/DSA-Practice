# Insertion Sort List (Medium)

## Problem Description

Given the head of a singly linked list, sort the list using **insertion sort**, and return the sorted list's head.

### **Steps of the Insertion Sort Algorithm**:

- Insertion sort iterates, consuming one input element in each repetition and growing a sorted output list.
- At each iteration, insertion sort **removes one element** from the input data, **finds the correct location** in the sorted list, and inserts it there.
- The process **repeats until no input elements remain**.

The following is a graphical example of the insertion sort algorithm:

- The **partially sorted list** (black) initially contains only the first element in the list.
- One element (**red**) is removed from the input data and inserted **in-place** into the sorted list in each iteration.

---

## **Examples**

### **Example 1**

**Input**:

```python
head = [4,2,1,3]
```

**Output**:

```python
[1,2,3,4]
```

### **Example 2**

**Input**:

```python
head = [-1,5,3,4,0]
```

**Output**:

```python
[-1,0,3,4,5]
```

## Constraints:

- The number of nodes in the list is in the range `[1, 5000]`.
- Each node's value satisfies `-5000 ≤ Node.val ≤ 5000`.

## Approach & Algorithm

- I have utilised a dummy node to be at the start of our list.
- The idea with the logic below is that we are looping through the list and if we find a number whereby `prev.next.val < cur.val` we move the `prev` pointer up till the point where the condition fails and the while loop breaks.
- We then rearrange where the pointers point (essentially attaching the node in place in the dummy list).
- View the written logic below:

![IMG_3223](https://github.com/user-attachments/assets/472f0b3d-47f8-4e1a-82d1-f8ba522ac806)
![IMG_3224](https://github.com/user-attachments/assets/d928c784-6f77-4424-9871-1fe4e84ca758)

## Code Implementation

### Solution:

- **Time Complexity:** O(n^2)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def insertionSortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(float('inf'))
        cur = head

        while cur:
            prev = dummy
            next_node = cur.next

            while prev.next and prev.next.val < cur.val:
                prev = prev.next

            # We insert here
            cur.next = prev.next        # Attaching to next node in dummy node list
            prev.next = cur
            cur = next_node

        return dummy.next
```
