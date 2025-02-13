# Last Stone Weight

---

## 🔗 Problem Statement

You are given an array of integers `stones` where `stones[i]` is the weight of the `i`th stone.

We are playing a game with the stones. On each turn, we choose the two heaviest stones and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed.
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has a new weight of `y - x`.

At the end of the game, there is at most **one stone left**.

Return the **weight of the last remaining stone**. If there are no stones left, return `0`.

---

## **Example 1**

**Input:**

```python
stones = [2,7,4,1,8,1]
```

**Output:**

```python
1
```

**Explanation:**

```python
We combine 7 and 8 to get 1, so the array becomes [2,4,1,1,1].
We combine 2 and 4 to get 2, so the array becomes [2,1,1,1].
We combine 2 and 1 to get 1, so the array becomes [1,1,1].
We combine 1 and 1 to get 0, so the array becomes [1].
The last remaining stone has weight 1.
```

## **Example 2**

**Input:**

```python
stones = [1]
```

**Output:**

```python
1
```

## Constraints

- `1 <= stones.length <= 30`
- `1 <= stones[i] <= 1000`

---

## Approach & Algorithm

- I have utilised the `heapq` module from python to assist me with this LC problem.
- This question required a **max-heap**, as we need to store the heaviest stone at the root, followed by stones that are lighter than it in its children (whilst we follow the order property).
- The `heapq` module does not actually work with max-heaps. So I utilised a hack whereby I negate the values from `stones` whilst pushing them into the heap. This would mean that our heap has negated values. Then when we pop the values to compare the stone weights I negate them again. This works due to the property of mathematics whereby two negatives make a positive -- `- - = +`.
- I continue looping through my `stones_by_max_weight` heap whilst it's length is greater than 1. Because at most our heap at the end will have 1 value as the spec states at the end there will be at most 1 stone remaining.
  - Whilst in the loop I pull two stones. The first stone will be the heaviest i.e., `stone_one_weight` or `y` as per the spec. Then I pop out `stone_two_weight` or `x` which will have a lesser weight than it's predecessor `stone_one_weight`.
  - We carry out evaluations to see if the stones have equal weight or if `stone_two_weight < stone_one_weight`. In the second case we carry out arithmetic to obtain the new value of `stone_two_weight` as the two stones were smashed together. In either case we push in a new value.
- We return the first and only element remaining in the array.

## Code Implementation

### Solution (DFS):

- **Time Complexity:** O(n \* log(k))

```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        stones_by_max_weight = []

        # We negate the stone values when storing (hack).
        # So when we pop we negate again to get positive value.
        for stone in stones:
            heapq.heappush(stones_by_max_weight, -stone)

        while len(stones_by_max_weight) > 1:
            # Negate the negated values whilst popping.
            stone_one_weight = -heapq.heappop(stones_by_max_weight)
            stone_two_weight = -heapq.heappop(stones_by_max_weight)

            if stone_one_weight == stone_two_weight:
                heapq.heappush(stones_by_max_weight, 0)
                continue

            if stone_two_weight < stone_one_weight:
                stone_two_weight = stone_two_weight - stone_one_weight
                heapq.heappush(stones_by_max_weight, stone_two_weight)

        return -stones_by_max_weight[0]
```
