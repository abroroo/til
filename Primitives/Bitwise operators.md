### What are Bitwise Operators?

Bitwise operators are used to manipulate individual bits of numbers. Computers store numbers in binary (which is a series of `1`s and `0`s), and bitwise operators allow us to directly work with these bits.

### Quick Recap:
- `&`: AND compares bits and returns `1` if both are `1`.
- `|`: OR compares bits and returns `1` if either bit is `1`.
- `^`: XOR returns `1` if the bits are different.
- `~`: NOT flips all bits (negation).
- `<<`: Left shift moves bits to the left (multiplication by 2).
- `>>`: Right shift moves bits to the right (division by 2).

---

**Example Problems**:

### **1. Check if a number is even or odd using the `&` operator**

**Code:**

```python
def is_odd(x):
    return (x & 1) == 1
```

**Explanation:**

- The bitwise AND operator `&` with `1` checks the least significant bit of the number.
  - If `x & 1` equals `1`, the number is **odd**.
  - If `x & 1` equals `0`, the number is **even**.

**Example:**

Checking if `5` is odd:

- Binary of `5` is `101`.
- `5 & 1` computes `101 & 001` which is `001` (binary for `1`).
- Since the result is `1`, `5` is **odd**.

**Test:**

```python
print(is_odd(5))  # Output: True
```

---

### **2. Flip the last bit of a number using the `^` operator**

**Code:**

```python
def flip_last_bit(x):
    return x ^ 1
```

**Explanation:**

- The bitwise XOR operator `^` with `1` flips the least significant bit:
  - If the last bit is `1`, it becomes `0`.
  - If the last bit is `0`, it becomes `1`.

**Example:**

Flipping the last bit of `9`:

- Binary of `9` is `1001`.
- `9 ^ 1` computes `1001 ^ 0001` which is `1000` (binary for `8`).
- So, flipping the last bit of `9` gives `8`.

**Test:**

```python
print(flip_last_bit(9))  # Output: 8
```

---

### **3. Multiply a number by 8 using the `<<` operator**

**Code:**

```python
def multiply_by_8(x):
    return x << 3
```

**Explanation:**

- The left shift operator `<<` moves bits to the left.
- Shifting left by `3` positions multiplies the number by \(2^3 = 8\).

**Example:**

Multiplying `5` by `8`:

- Binary of `5` is `101`.
- `5 << 3` shifts bits to `101000` (binary for `40`).
- So, `5 << 3` equals `40`.

**Test:**

```python
print(multiply_by_8(5))  # Output: 40
```

---

