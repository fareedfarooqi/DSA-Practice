# Longest Substring Without Repeating Characters (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**3. Longest Substring Without Repeating Characters**](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

## **Problem Statement**

Given a string `s`, find the length of the **longest substring** without **duplicate characters**.

---

## **Example 1**

**Input:**
```python
s = "abcabcbb"
```

**Output:**
```python
3
```

**Explanation:**
- The longest substring without repeating characters is `"abc"` with length 3.

## **Example 2**

**Input:**
```python
s = "bbbbb"
```

**Output:**
```python
1
```

**Explanation:**
- The longest substring is `"b"` with length 1.

## **Example 3**

**Input:**
```python
s = "pwwkew"
```

**Output:**
```python
3
```

**Explanation:**
- The longest substring is `"wke"` with length 3.
- Note: `"pwke"` is a subsequence, not a substring.

---

## **Constraints**

- `0 <= s.length <= 5 * 10⁴`
- `s` consists of English letters, digits, symbols, and spaces.

---

## Approach & Algorithm:

- In all solutions below I've utilised some form of a variable sliding window algorithm.
- Solution one is faster with a linear time complexity. This is due to the fact that we utilise sets with a two pointer approach. Sets have the amazing property that lookups in sets is of `O(1)` (constant) time complexity as compared to using a double-ended queue as per solution three.
- In solution one we utilise two pointers `L` and `R` to keep track of the window itself. We loop through the string `s` and we check to see if the current character `s[R]` is not in the characters set `charSet`. If it is not then we simply add the current character to the set. Otherwise we check to see if the length of the character set is greater than 0 (not ideal as per solution two). We then simply loop through the set of characters and remove the character pointed to by our left pointer `L` in the string from the character set `charSet`. We then shift the left pointer up by one and keep going until we have a valid window. After this we simply add the latest character from the original loop to the set.
- We then check to see if the longest substring was found.
- **NOTE:** Solution two is the **fastest** solution. It is like solution one but we cut out a lot of the fluff to speed up the algorithm.

## Code Implementation:

### Solution One (FASTER):

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(k)`

```python
from collections import deque

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        L, longestSubStr, charsSet = 0, 0, set()

        for R in range(len(s)):
            if s[R] not in charsSet:
                charsSet.add(s[R])
            elif len(charsSet) > 0:
                # Current character we are looping over is already in the charsQueue.
                # We must slide the window forward to the right.
                # We must pop the leftmost value.

                while s[R] in charsSet:
                    # We must reset the window by sliding the entire window upto R.
                    charsSet.remove(s[L])
                    L += 1
                
                charsSet.add(s[R])
            
            longestSubStr = max(longestSubStr, len(charsSet))

        return longestSubStr
```

### Solution Three (SLOWER):

- **Time Complexity:** `O(n^2)`
- **Space Complexity:** `O(k)`

```python
from collections import deque

class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        L, longestSubStr, charsQueue = 0, 0, deque()

        for R in range(len(s)):
            if s[R] not in charsQueue:
                charsQueue.append(s[R])
            elif len(charsQueue) > 0:
                # Current character we are looping over is already in the charsQueue.
                # We must slide the window forward to the right.
                # We must pop the leftmost value.
                charsQueue.popleft()

                while s[R] in charsQueue:
                    # We must reset the window by sliding the entire window upto R.
                    charsQueue.popleft()
                
                charsQueue.append(s[R])
            
            longestSubStr = max(longestSubStr, len(charsQueue))
        

        print(charsQueue)
        return longestSubStr
```