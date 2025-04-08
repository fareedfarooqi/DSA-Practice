# Longest Repeating Character Replacement (Medium)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**424. Longest Repeating Character Replacement**](https://leetcode.com/problems/longest-repeating-character-replacement/)

---

## Problem Statement

You are given a string `s` and an integer `k`. You can choose **any character** of the string and **change it** to **any other uppercase English character**. You can perform this operation at most `k` times.

Return the **length of the longest substring** containing the **same letter** you can get after performing the above operations.

---

## Example 1

**Input:**

```python
s = "ABAB"
k = 2
```

**Output:**

```python
4
```

**Explanation:**

```plaintext
Replace the two 'A's with two 'B's or vice versa.
The entire string becomes all the same character.
```

## Example 2

**Input:**

```python
s = "AABABBA"
k = 1
```

**Output:**

```python
4
```

**Explanation:**

```plaintext
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may be other ways to reach the answer as well.
```

---

## Constraints:

- `1 <= s.length <= 10⁵`
- `s consists of only uppercase English letters`
- `0 <= k <= s.length`

---

## Approach & Algorithm

- I've utilised a variable sliding window algorithm to solve this question.
- They key to solving this question is to understand that we do **NOT** need to physically replace the characters in the string. We merely need to check if we **can** change characters in the string at most `k` times.
- To achieve this I've utilised a hashmap - `countOfChars` whereby I keep track of the character in the current window and the number of times we have seen this character within the current window.
- We also utilise a left and right pointer, `L` and `R` respectively to keep track of the window itself.
- Our variable `length` will keep track of the longest subarray we can make as per the criteria in the question.
- My intuition was that we can find the most frequently occurring character within a window (`mostFrequentCharCount`) and we can subtract that from the length of the current window (`lengthOfCurWindow`). This will give us the result for the number of characters we need to replace in order to match it with the most frequently occurring character. So if we have in our current window `AABA`, our `countOfChars` will look like the following:

```python
countOfChars = {
    'A': 3,
    'B': 1
}
```

- As we can see the `mostFrequentCharCount` is `3` with the most frequently occurring character being `A`. So in our window we do `lengthOfCurWindow - mostFrequentCharCount` --> `4 - 3 = 1`. Then we can check if `1` is less than or equal to `k` (let `k = 1`). This will mean that we need to replace at most one character in our current window i.e., change `B` to an `A` giving us `AAAA`. This is a valid window as our window contains all the same characters whilst ensuring that we changed at most `k` characters.

## Code Implementation:

### Solution One (Sliding Window Algorithm):

- **Time Complexity:** `O(26 * n)` --> `O(n)`

```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        # We don't actually need to physically replace the character in the string.
        countOfChars = defaultdict(int)
        L = 0
        length = 0

        for R in range(len(s)):
            countOfChars[s[R]] += 1

            # Get the count of the least frequently occuring character in the window.
            # We could write: mostFrequentChar = max(countOfChars, key=countOfChars.get)
            # We could write: mostFrequentCharCount = countOfChars[mostFrequentChar]

            mostFrequentCharCount = max(countOfChars.values())
            lengthOfCurWindow = R - L + 1

            if lengthOfCurWindow - mostFrequentCharCount <= k:
                # Means we have to replace at most 'charCount' characters.
                length = max(length, lengthOfCurWindow)
                continue

            # Otherwise it means we cannot replace characters within 'k' counts.
            # We must slide the window and adjust the hashmap counts of the characters in the window.

            countOfChars[s[L]] -= 1
            L += 1

        return length
```
