# Design Linked List

## Problem Description

Design your implementation of the linked list. You can choose to use a **singly** or **doubly** linked list. A node in a singly linked list should have two attributes:

- `val`: the value of the current node.
- `next`: a pointer/reference to the next node.

If you want to use a doubly linked list, you will need one more attribute:

- `prev`: a pointer/reference to the previous node.

Assume all nodes in the linked list are **0-indexed**.

Implement the `MyLinkedList` class:

- `MyLinkedList()`: Initializes the `MyLinkedList` object.
- `int get(int index)`: Get the value of the `index`th node in the linked list. If the index is invalid, return `-1`.
- `void addAtHead(int val)`: Add a node of value `val` **before the first element** of the linked list. After the insertion, the new node will be the first node of the linked list.
- `void addAtTail(int val)`: Append a node of value `val` as the **last element** of the linked list.
- `void addAtIndex(int index, int val)`: Add a node of value `val` **before the `index`th node** in the linked list. If `index` equals the length of the linked list, the node will be appended to the end of the linked list. If `index` is greater than the length, the node will not be inserted.
- `void deleteAtIndex(int index)`: Delete the `index`th node in the linked list, if the index is valid.

---

## Examples

### Example 1:

**Input**:
`["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]`
`[[], [1], [3], [1, 2], [1], [1], [1]]`

**Output**:
`[null, null, null, null, 2, null, 3]`

**Explanation**:
MyLinkedList myLinkedList = new MyLinkedList();
myLinkedList.addAtHead(1); // linked list becomes 1
myLinkedList.addAtTail(3); // linked list becomes 1->3
myLinkedList.addAtIndex(1, 2); // linked list becomes 1->2->3
myLinkedList.get(1); // return 2
myLinkedList.deleteAtIndex(1); // now the linked list is 1->3
myLinkedList.get(1); // return 3

## Constraints

- `0 <= index, val <= 1000`
- At most `2000` calls will be made to `get`, `addAtHead`, `addAtTail`, `addAtIndex`, and `deleteAtIndex`.

---

## Approach & Algorithms

### 1. Doubly Linked List Implementation

#### **Data Structure**:

- Use a `ListNode` class to define each node in the linked list, with the attributes `val`, `prev`, and `next`.
- Use a `MyLinkedList` class to manage the linked list, with a `head` pointer to the start of the list.

#### **Operations**:

1. **`get(index)`**:

   - Traverse the list from the `head` and return the value of the node at the specified `index`.
   - Return `-1` if the index is out of bounds.

2. **`addAtHead(val)`**:

   - Create a new node with the given `val`.
   - Update the `prev` pointer of the current `head`, and make the new node the `head`.

3. **`addAtTail(val)`**:

   - Traverse to the last node.
   - Append the new node after it, updating both `next` and `prev` pointers.

4. **`addAtIndex(index, val)`**:

   - If the `index` is `0`, use `addAtHead`.
   - Traverse to the `index - 1` node and insert the new node between the `prev` and `current`.

5. **`deleteAtIndex(index)`**:
   - If the `index` is `0`, update `self.head` to the next node.
   - For other indices, update the `prev` and `next` pointers of the surrounding nodes to bypass the deleted node.

---

## Code Implementation

### Python Implementation

- **Time Complexity:** O(n + m) --> We need to traverse two linked lists.

```python
class MyLinkedList:

    def __init__(self):
        self.head = None

    def get(self, index: int) -> int:
        current = self.head
        count = 0

        while current is not None:
            if count == index:
                return current.val
            current = current.next
            count += 1

        return -1

    def addAtHead(self, val: int) -> None:
        new_node = ListNode(val, None, self.head)
        if self.head is not None:
            self.head.prev = new_node
        self.head = new_node

    def addAtTail(self, val: int) -> None:
        if self.head is None:
            self.head = ListNode(val, None, None)
            return

        current = self.head
        while current.next is not None:
            current = current.next

        current.next = ListNode(val, current, None)

    def addAtIndex(self, index: int, val: int) -> None:
        if index == 0:  # Insert at head
            self.addAtHead(val)
            return

        current = self.head
        cur_index = 0

        while current is not None:
            if cur_index == index:
                new_node = ListNode(val, current.prev, current)
                if current.prev is not None:
                    current.prev.next = new_node
                current.prev = new_node
                return

            current = current.next
            cur_index += 1

        if cur_index == index:  # Append at tail
            self.addAtTail(val)

    def deleteAtIndex(self, index: int) -> None:
        if self.head is None:
            return  # Empty list

        if index == 0:  # Delete the head
            self.head = self.head.next
            if self.head is not None:
                self.head.prev = None
            return

        current = self.head
        cur_index = 0

        while current is not None:
            if cur_index == index:
                if current.next is not None:
                    current.next.prev = current.prev
                if current.prev is not None:
                    current.prev.next = current.next
                return
            current = current.next
            cur_index += 1


class ListNode:
    def __init__(self, val=0, prev=None, next=None):
        self.val = val
        self.prev = prev
        self.next = next
```
