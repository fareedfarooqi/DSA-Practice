# Reverse Bits (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**190. Reverse Bits**](https://leetcode.com/problems/reverse-bits/)

---

## **Problem Statement**

Reverse the bits of a given **32-bit unsigned integer**.

---

## **Note**

- In some languages (like Java), there is no unsigned integer type. In such cases, both input and output will be given as signed integers.
- This does **not affect the implementation**, because the **internal binary representation is the same**, whether signed or unsigned.
- In Java, signed integers use **2's complement notation**, so values like `-3` may appear as large unsigned numbers when reversed.

---

## **Example 1**

**Input:**
```plaintext
n = 00000010100101000001111010011100
```

**Output:**
```plaintext
964176192 (00111001011110000010100101000000)
```

**Explanation:**
The input binary string represents the unsigned integer `43261596`.  
Its reversed binary is `00111001011110000010100101000000`, which equals `964176192`.

---

## **Example 2**

**Input:**
```plaintext
n = 11111111111111111111111111111101
```

**Output:**
```plaintext
3221225471 (10111111111111111111111111111111)
```

**Explanation:**
The input binary string represents the unsigned integer `4294967293`.  
Its reversed binary is `10111111111111111111111111111111`, which equals `3221225471`.

---

## **Constraints**

- The input must be a **binary string of length 32**

---

## Approach & Algorithm:

- The trick to solving this question is to using bit manipulation.
- We loop through all `32` bits and for each bit we shift it right by `i` bits (0 to 32 bits). We `&` it with `1` to get the last value.
- After this we construct our `res` by appending each `bit` previously and shift it left by `31 - i` bits. So if the bit is `1` and `i = 0`, then `res = 1000 0000 0000 0000 0000 0000 0000 0000`. So if the bit is `1` and `i = 1`, then `res = 1100 0000 0000 0000 0000 0000 0000 0000`.

## Code Implementation:

### Solution One:

- **Time Complexity:** `O(1)`

```python
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        for i in range(32):
            bit = (n >> i) & 1
            res += ((bit << (31 - i)))
        
        return res

```

### Solution Two:

- **Time Complexity:** `O(1)`

```python
class Solution:
    def reverseBits(self, n: int) -> int:
        newNumBits = 0

        for i in range(32):
            if n & 1 == 1:
                newNumBits = (newNumBits << 1) | 1
            else:
                newNumBits = (newNumBits << 1) | 0
            n = n >> 1

        return newNumBits
```
