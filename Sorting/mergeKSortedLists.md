# Merge k Sorted Lists (Hard)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Merge k Sorted Lists**](https://leetcode.com/problems/merge-k-sorted-lists/description/)

---

## Problem Description

You are given an array of **k** linked lists, where each linked list is sorted in **ascending order**.

Merge all the linked lists into **one sorted linked list** and return the head of the merged list.

---

## **Examples**

### **Example 1**

**Input**:

```python
lists = [[1,4,5],[1,3,4],[2,6]]
```

**Output**:

```python
[1,1,2,3,4,4,5,6]
```

**Explanation**: The linked lists are:

```python
[
  1 -> 4 -> 5,
  1 -> 3 -> 4,
  2 -> 6
]
```

Merging them into one sorted list:

```python
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
```

### **Example 2**

**Input**:

```python
lists = []
```

**Output**:

```python
[]
```

### **Example 3**

**Input**:

```python
lists = [[]]
```

**Output**:

```python
[]
```

## Constraints

- `k == lists.length`
- `0 <= k <= 10⁴`
- `0 <= lists[i].length <= 500`
- `-10⁴ <= lists[i][j] <= 10⁴`
- `lists[i]` is sorted in ascending order.
- The sum of `lists[i].length` will not exceed `10⁴`.

---

## Approach & Algorithm

- One solution I observed was breaking the problem down into sub-problems. So the core logic goes as follows.
- We need to combine all the linked lists in `lists` into one linked list. The way to do it is to work from left to right.
- So we increment our loop by **two**, whereby we attempt to merge two lists at a time --> `lists[i]` and `lists[i + 1]`. (Handle edge cases appropriately).
- We have a secondary function called **mergeList()** that allows us to merge `lists[i]` and `lists[i + 1]`.
- We keep merging these linked lists until we only have 1 linked list in the `lists` remaining.
- The logic in **mergeList()** is self-explanatory and follows the **dummy-node** approach.

## Code Implementation

### Solution:

- **Time Complexity:** O(n\*log(k))

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if not lists or len(lists) == 0:
            return None

        while len(lists) > 1:
            mergedLists = []
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i + 1] if (i + 1) < len(lists) else None
                mergedLists.append(self.mergeList(l1, l2))
            lists = mergedLists
        return lists[0]

    def mergeList(self, l1, l2):
        dummy = ListNode(float('inf'))
        tail = dummy

        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            elif l2.val <= l2.val:
                tail.next = l2
                l2 = l2.next
            tail = tail.next

        if l1:
            tail.next = l1
        if l2:
            tail.next = l2

        return dummy.next
```
