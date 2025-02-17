# LRU Cache

---

## 🔗 Problem Statement

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)`: Initializes the LRU cache with positive size `capacity`.
- `int get(int key)`: Returns the value of the `key` if the `key` exists, otherwise returns `-1`.
- `void put(int key, int value)`: Updates the value of the `key` if the `key` exists. Otherwise, adds the `key-value` pair to the cache. If the number of keys exceeds the `capacity`, it evicts the **least recently used** key.

The functions `get` and `put` must each run in **O(1) average time complexity**.

---

## **Example 1**

**Input:**

```python
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
```

**Output:**

```python
[null, null, null, 1, null, -1, null, -1, 3, 4]
```

**Explanation:**

```plaintext
lRUCache = LRUCache(2)
lRUCache.put(1, 1)  # cache is {1=1}
lRUCache.put(2, 2)  # cache is {1=1, 2=2}
lRUCache.get(1)     # returns 1
lRUCache.put(3, 3)  # LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2)     # returns -1 (not found)
lRUCache.put(4, 4)  # LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1)     # returns -1 (not found)
lRUCache.get(3)     # returns 3
lRUCache.get(4)     # returns 4
```

## Constraints

- `1 <= capacity <= 3000`
- `0 <= key <= 10⁴`
- `0 <= value <= 10⁵`
- At most `2 * 10⁵` calls will be made to `get` and `put`.

---

## Approach & Algorithm

- The trick to solving this question was to truly understand the [LRU Caching Algorithm](https://www.geeksforgeeks.org/lru-cache-implementation/).
- I utilised a hasp map - `cache` and a double-ended-queue `cachePriorityQueue`.
  - `cache` allowed me to store the values corresponding to their respective keys in an efficient manner. The `cache` hash map allowed me to insert, remove and search for values in constant time (O(1)).
  - `cachePriorityQueue` was a double-ended-queue that allowed me to create and leverage a data structure whereby I could keep the **right-hand-side** of the `cachePriorityQueue` strictly for new items (which are automatically high priority). The **left-hand-side** of the `cachePriorityQueue` was for older items that were not called frequently and as such were of lesser priority than the items in the right-hand-side of the cache queue.

## Code Implementation

### Solution:

- **Time Complexity:** O(n). But can be O(1) for small data sets.

```python
from collections import deque

class LRUCache:

    def __init__(self, capacity: int):
        self.cache = {}
        self.cachePriorityQueue = deque(maxlen=capacity)

    def get(self, key: int) -> int:
        if key in self.cache:
            self.cachePriorityQueue.remove(key)
            self.cachePriorityQueue.append(key)
            return self.cache[key]

        return self.cache.get(key, -1)

    def put(self, key: int, value: int) -> None:
        if key not in self.cache and len(self.cachePriorityQueue) == self.cachePriorityQueue.maxlen:
            # We now need to pop the least used element from our cache.
            # They way I've structured it is that our first element is
            # our least used element.
            elementToRemove = self.cachePriorityQueue.popleft()
            del self.cache[elementToRemove]

            # Now we can insert the new element as there is space.
            self.cachePriorityQueue.append(key)
            self.cache[key] = value
        elif key not in self.cache:

            self.cachePriorityQueue.append(key)
            self.cache[key] = value
        elif key in self.cache:
            # If the value is in our cache map we must replace it. As per test case we
            # must override the value associated with this key.
            self.cache[key] = value

            # We must also update it's positioning in the cache queue.
            self.cachePriorityQueue.remove(key)
            self.cachePriorityQueue.append(key)

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
