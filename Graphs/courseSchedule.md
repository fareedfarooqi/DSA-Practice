# Course Schedule (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Course Schedule**](https://leetcode.com/problems/course-schedule/)

---

## Problem Statement

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`.  
You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

For example, the pair `[0, 1]` indicates that to take course `0`, you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

---

## **Example 1**

**Input:**

```python
numCourses = 2
prerequisites = [[1,0]]
```

**Output:**

```python
true
```

**Explanation::**

```plaintext
There are a total of `2` courses to take.
To take course `1`, you should have finished course `0`.
Since there are no cycles, it is possible to finish all courses.
```

## **Example 2**

**Input:**

```python
numCourses = 2
prerequisites = [[1,0],[0,1]]
```

**Output:**

```python
false
```

**Explanation::**

```plaintext
There are a total of `2` courses to take.
To take course `1`, you should have finished course `0`, and to take course `0`, you should also have finished course `1`.
Since this forms a cycle, it is impossible to finish all courses.
```

## Constraints

- `1 <= numCourses <= 2000`
- `0 <= prerequisites.length <= 5000`
- `prerequisites[i].length == 2`
- `0 <= ai, bi < numCourses`
- All the pairs `prerequisites[i]` are unique.

---

## Approach & Algorithm

- I utilised an adjacency list DFS implementation to solve this problem.
- I first and foremost created a `preMap` which essentially stores the node as a key which has the value of a list of other nodes to indicate where the key node is directed towards, i.e., what are the nodes prerequisites.
- We have an entry point into the graph which is via the final loop in the solution below. However, from there we have a gateway into traversing the graph. if at any point we observe that the node being inserted into the `visited` set we know we have found a duplicate and as such we return false.
- `Solution One` is the optimised working solution as it has a memoized approach. In essence we clear the prerequisites of a given node from the `preMap` if we found no cycle whilst traversing it's path. The reason being this helps us by not having to recompute each and every node repeatedly.
- Please view my drawn out approach on whiteboard below:

<img width="973" alt="Screenshot 2025-03-12 at 10 46 35 PM" src="https://github.com/user-attachments/assets/02245f29-1281-492c-961a-0055984deafc" />

## Code Implementation

### Solution One:

- **Time Complexity:** O(V + E).

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        preMap = {i: [] for i in range(numCourses)}

        for course, prereq in prerequisites:
            preMap[course].append(prereq)

        visited = set()

        def dfs(course):
            if course in visited:
                return False # We found a loop.

            if preMap[course] == []:
                # Meaning we are at the base course i.e., there is no prerequisites
                # in order to do this particular course.
                return True

            visited.add(course)

            for prereq in preMap[course]:
                if not dfs(prereq):
                    return False

            preMap[course] = [] # We are eseentially caching our solution (memoization).
            visited.remove(course)
            return True

        for course in range(numCourses):
            if not dfs(course):
                # Our DFS returned False meaning there is a cycle.
                return False

        return True # We found no cycle.
```

### Solution Two (Slower - TLE):

- **Time Complexity:** O(V + E).

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        preMap = {i: [] for i in range(numCourses)}

        for course, prereq in prerequisites:
            preMap[course].append(prereq)

        visited = set()

        def dfs(course):
            if course in visited:
                return False # We found a loop.

            if preMap[course] == []:
                # Meaning we are at the base course i.e., there is no prerequisites
                # in order to do this particular course.
                return True

            visited.add(course)

            for prereq in preMap[course]:
                if not dfs(prereq):
                    return False

            visited.remove(course)
            return True

        for course in range(numCourses):
            if not dfs(course):
                # Our DFS returned False meaning there is a cycle.
                return False

        return True # We found no cycle.
```
