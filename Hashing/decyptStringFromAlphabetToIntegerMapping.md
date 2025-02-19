# Decrypt String from Alphabet to Integer Mapping

---

## 🔗 Problem Statement

You are given a string `s` formed by digits and `#`. We want to map `s` to English lowercase characters as follows:

- Characters ('a' to 'i') are represented by ('1' to '9') respectively.
- Characters ('j' to 'z') are represented by ('10#' to '26#') respectively.

Return the string formed after mapping.

The test cases are generated so that a unique mapping will always exist.

---

## **Example 1**

**Input:**

```python
s = "10#11#12"
```

**Output:**

```python
"jkab"
```

**Explanation:**

```plaintext
"10#" -> "j"
"11#" -> "k"
"1"   -> "a"
"2"   -> "b"
```

## **Example 2**

**Input:**

```python
s = "1326#"
```

**Output:**

```python
"acz"
```

**Explanation:**

```plaintext
"1"    -> "a"
"3"    -> "c"
"26#"  -> "z"
```

## Constraints

- `1 <= s.length <= 1000`
- `s` consists of digits and the `#` character.
- `s` will be a valid string such that mapping is always possible.

---

## Approach & Algorithm

- I utilised a hash map to solve this problem.
- I created a hash map `dic` whereby I zip up two independent lists of numbers from `[1, ..., 26]` and characters from `[a, ..., z]`. The key of our hash map are the numbers and the values are the letters.
  - `string.ascii_lowercase` simply returns a string of charcters from `a-z`.
- I've also created an `i` pointer that keeps track of where we are whilst looping through our `s` string. I also have a `result_str` which we use to append characters that pass the conditions.
- We loop until our `i` pointer has reached the end of the string `s`.
  - Through the loop we check if the third character (`i + 2`) is equal to `#`. This tells us if we are now going to be processing a double-digit element i.e., `10#`. If this is the case we simply find the corresponding value for the key `10` in our `dic` hash map and append it to our `result_str`.
  - Otherwise we know that we are processing a single-digit element such as `1-9`. We similarly get the key-value mapping from our `dic` hash map and append it to our `result_str`.
- **Note:** Problem with our first solution below is that in Python, strings are immutable, so "result_str += ..." takes O(n) over multiple iterations as it creates a new copy of the result string every iteration (meaning it loops over every character `n` times). So in solution 2, I utilise lists and the `join()` function to speed up the solution.

## Code Implementation

### Solution 1 (Slower):

- **Time Complexity:** O(n^2).

```python
import string

class Solution:
    def freqAlphabets(self, s: str) -> str:
        dic = dict(zip(range(1, 27), string.ascii_lowercase))
        i, result_str = 0, ''

        while i < len(s):
            if i + 2 < len(s) and s[i + 2] == "#":
                result_str += dic[int(s[i:i + 2])]
                i += 3
            else:
                result_str += dic[int(s[i])]
                i += 1

        return result_str
```

### Solution 2 (Faster):

- **Time Complexity:** O(n).

```python
import string

class Solution:
    def freqAlphabets(self, s: str) -> str:
        dic = dict(zip(range(1, 27), string.ascii_lowercase))
        i, result = 0, []

        while i < len(s):
            if i + 2 < len(s) and s[i + 2] == "#":
                result.append(dic[int(s[i:i + 2])])
                i += 3
            else:
                result.append(dic[int(s[i])])
                i += 1

        return "".join(result)
```
