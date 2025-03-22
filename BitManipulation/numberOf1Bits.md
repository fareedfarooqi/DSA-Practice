# Number of 1 Bits (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**191. Number of 1 Bits**](https://leetcode.com/problems/number-of-1-bits/)

---

## **Problem Statement**

Given a positive integer `n`, write a function that returns the number of **set bits** in its **binary representation** (also known as the **Hamming weight**).

---

## **Example 1**

**Input:**
```python
n = 11
```

**Output:**

```python
3
```

**Explanation:**
The input binary string `1011` has a total of three set bits.

## **Example 2**

**Input:**
```python
n = 128
```

**Output:**

```python
1
```

**Explanation:**
The input binary string `10000000` has a total of one set bit.

## **Example 3**

**Input:**
```python
n = 2147483645
```

**Output:**

```python
30
```

**Explanation:**
The input binary string `1111111111111111111111111111101` has a total of thirty set bits.

## Constraints

- `1 <= n <= 2³¹ - 1`

---

## Approach & Algorithm:

- I've utilised bit manipulation to solve this question.
- The trick to doing this question is understanding the fact that we can use the logical operators `&` and `<<`.
- We can loop through the bits of the number `n` until we get `n == 0`. We do a logical `&` with `n` and `1` to see if the last bit is 1 or not. If it is 1 we know that we have found a 1 bit and can increment our count.
- Note:
```plaintext
    1 0 1 1 1
  & 0 0 0 0 1
    ---------
    0 0 0 0 1
```

## Code Implementation

### Solution:

- **Time Complexity:** `O(log(n))` --> We divide by 2 for each iteration (halving the problem space)

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0

        # While our number 'n' is not zero (has some non-zero bits).
        while n > 0:
            print(n)
            if n & 1 == 1:
                # Means that the last bit was '1' indicating the number is '1'
                # and thus that we have found a '1' bit.
                count += 1
            
            # Otherwise we need to shift right by one to move the last bit we checked
            # out of the scope.
            n = n >> 1
        
        return count