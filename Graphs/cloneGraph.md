# Clone Graph (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**133. Clone Graph**](https://leetcode.com/problems/clone-graph/)

---

## Problem Statement

Given a reference of a node in a **connected** **undirected** graph, return a **deep copy (clone)** of the graph.

Each node in the graph contains:
- A value (`int`)
- A list (`List[Node]`) of its neighbors.

```java
class Node {
    public int val;
    public List<Node> neighbors;
}
```

The input graph is given as an adjacency list.

- Each node's value is the same as its **1-based index**.
- The given node will always be the first node (`val = 1`).
- The graph is connected, meaning all nodes can be visited starting from `node 1`.

---

## **Example 1**

**Input:**

```python
adjList = [[2,4],[1,3],[2,4],[1,3]]
```

**Output:**
```python
[[2,4],[1,3],[2,4],[1,3]]
```

**Explanation:**
```plaintext
There are 4 nodes in the graph:
- 1st node's neighbors are [2,4]
- 2nd node's neighbors are [1,3]
- 3rd node's neighbors are [2,4]
- 4th node's neighbors are [1,3]
```

## **Example 2**

**Input:**

```python
adjList = [[]]
```

**Output:**
```python
[[]]
```

**Explanation:**
```plaintext
The graph consists of one node (val = 1) with no neighbors.
```

## **Example 3**

**Input:**

```python
adjList = []
```

**Output:**
```python
[]
```

**Explanation:**
```plaintext
The graph is empty (no nodes).
```

## Constraints

- `n == grid.length`
- `n == grid[i].length`
- `1 <= n <= 100`
- `grid[i][j] is 0 or 1.`

---

## Approach & Algorithm

- I've utilised a DFS approach in order to solve this question.
- I created a hash map `old_to_new` which was used to keep a mapping of old nodes to new nodes (including neighbours).
  - `old_to_new = { old_node1: copy1, old_node2: copy2, old_node3: copy3, old_node4: copy4 }`, where `old_node` and `copy` are full nodes with their respective values and neighbours.
- I carried out a DFS algorithm and went deep into the graph in order to reconstruct the undirected edges between the nodes.

## Code Implementation

### Solution:

- **Time Complexity:** O(V + E).

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

from typing import Optional
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if node is None:
            return

        old_to_new = {}

        def dfs(node):
            if node in old_to_new:
                return old_to_new[node]
            
            # Otherwise node is not in our hash map.
            copy = Node(node.val)
            old_to_new[node] = copy

            for neighbor in node.neighbors:
                copy.neighbors.append(dfs(neighbor))
            
            return copy
        
        return dfs(node)
```