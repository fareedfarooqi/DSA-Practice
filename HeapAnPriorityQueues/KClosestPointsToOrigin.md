# K Closest Points to Origin (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**K Closest Points to Origin**](https://leetcode.com/problems/k-closest-points-to-origin/)

---

## Problem Statement

You are given a set of points on a 2D plane and must find the `k` closest points to the **origin (0,0)** using **Euclidean distance**.

The distance between two points on the X-Y plane is given by:

\[
\sqrt{(x_1 - 0)^2 + (y_1 - 0)^2}
\]

You must return the `k` closest points in **any order**.

### **Implement the function:**

- `List[List[int]] kClosest(List[List[int]] points, int k)`:  
  Given a list of points, return the `k` closest points to the origin `(0,0)`.

---

## **Example 1**

![1](https://github.com/user-attachments/assets/f082e24d-32f1-4ae0-88d9-7c3c0f362311)

**Input:**
```python
points = [[1,3],[-2,2]]
k = 1
```

**Output:**
```python
[[-2,2]]
```

**Explanation:**
```plaintext
Distance of (1,3) from origin = sqrt(1^2 + 3^2) = sqrt(10)
Distance of (-2,2) from origin = sqrt((-2)^2 + 2^2) = sqrt(8)
Since sqrt(8) < sqrt(10), (-2,2) is closer.
We only need the 1 closest point, so output is [[-2,2]].
```

## **Example 2**

**Input:**
```python
points = [[1,3],[-2,2]]
k = 1
```

**Output:**
```python
[[-2,2]]
```

**Explanation:**
```plaintext
Distances:
(3,3)   → sqrt(18)
(5,-1)  → sqrt(26)
(-2,4)  → sqrt(20)

The two closest points are (3,3) and (-2,4).
Order can vary, so [[-2,4],[3,3]] is also correct.
```

Constraints
1 <= k <= points.length <= 10^4
-10^4 <= xi, yi <= 10^4

## Constraints

- `1 <= k <= points.length <= 10^4`
- `10^4 <= xi, yi <= 10^4`

---

## Approach & Algorithm
- The trick to this question was noticing that it required a **min-heap** and as such I utilised the **heapq** module.
- I utilised two additional lists `euclideanDistances` which was used to store all the Euclidean Distances from the origin for each point in `points` list. I also utilised `finalKPoints` list which was our list to return that stored the `k` lists that are closest in terms of distance to the origin. I also utilised a dict `euclideanPointsToDistanceMapping`. This dictionary was very useful as I used key-value mapping whereby I stored the `euclideanDistance` of each point as a key and then stored the point it self in a list of lists. So for example:
  - `points = [[0,1],[1,0]]`, and `k = 2`. Both of these points will have the same Euclidean Distance of `1.0`. As such we need to store both the points `[0,1],[1,0]` in our dictionary with the corresponding key of `1.0`. We will thus have a dict of `{1.0: [[0, 1], [1, 0]]}`.
- The line `heapq.heapify(euclideanDistances)` allows us to create a **min-heap** whereby the root is always the smallest distance. Then in our `euclideanPointsToDistanceMapping` the root from our euclideanDistances **min-heap** will correspond to the closest point to the origin.

## Code Implementation

### Solution One - (Heap + Dict Approach):

- **Time Complexity:** O(n \* log(k))

```python
import heapq
import math

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        # What we can do is we get a list of points, we can 
        # loop through the list of points and calculate the Euclidean Distance
        # for each of the points from the origin. We store these in a list
        # and once that is done we can 'heapify' it and return 'k' of the points.
        
        euclideanDistances = []
        euclideanPointsToDistanceMapping = {}

        for x, y in points:
            euclideanDistance = math.sqrt((x - 0) ** 2 + (y - 0) ** 2)
            euclideanDistances.append(euclideanDistance)

            if euclideanDistance in euclideanPointsToDistanceMapping:
                euclideanPointsToDistanceMapping[euclideanDistance].append([x, y])
            else:
                euclideanPointsToDistanceMapping[euclideanDistance] = [[x, y]]

        heapq.heapify(euclideanDistances)
        
        finalKPoints = []

        while len(finalKPoints) < k:
            euclideanDistance = heapq.heappop(euclideanDistances)
            for point in euclideanPointsToDistanceMapping[euclideanDistance]:
                finalKPoints.append(point)

        return finalKPoints
```

### Solution Two - Pure Heap Approach

- **Time Complexity:** O(n \* log(k))
- **Note:** More Space Efficient. Also a heap in python can store a tuple too. So this means we can store (distance, point) in heap. Note heap sorts on the first element.

```python
import heapq
import math

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        heapOfCoordinatesWithDistances = []
        
        for point in points:
            euclideanDistance = math.sqrt((point[0] - 0)**2 + (point[1] - 0)**2)
            heapq.heappush(heapOfCoordinatesWithDistances, (-euclideanDistance, point))

        while len(heapOfCoordinatesWithDistances) > k:
            heapq.heappop(heapOfCoordinatesWithDistances)

        closestCoordinates = []
        for i in range(k):
            shortestDistanceTuple = heapq.heappop(heapOfCoordinatesWithDistances)
            closestCoordinates.append(shortestDistanceTuple[1])
        
        return closestCoordinates
```


