### What is the "Lowermost Set Bit"?

The **lowermost set bit** (or **least significant set bit**) is the **first `1` you encounter** when looking at a binary number from right to left. In other words, it's the rightmost bit that is `1`.

#### Example:
For `x = 18` (binary `10010`):
- The lowermost set bit is `1` at the 2nd position from the right (starting from 0).

### Why do we care about the lowermost set bit?
Manipulating the lowermost set bit is useful in various algorithms like finding subsets, counting bits, or working with binary representations efficiently.

### Key Rules:
- **Subtracting 1** from a number flips the last `1` to `0` and turns any trailing `0`s into `1`s.
- **Adding 1** to a number flips the last `0` to `1` and turns any trailing `1`s into `0`s.
  
---

### Operations on the Lowermost Set Bit:

1. **Clear the Lowermost Set Bit**:
   - **What it does**: Turns the rightmost `1` into a `0`.
   - **How**: `x & (x - 1)`
   
   #### Example:
   For `x = 18` (binary `10010`):
   ```
   x - 1 = 17 (binary 10001)
   x & (x - 1) = 10010 & 10001 = 10000
   ```
   The result is `10000` (16 in decimal), where the rightmost `1` has been cleared.

2. **Set the Lowermost `0`**:
   - **What it does**: Turns the rightmost `0` into a `1`.
   - **How**: `x | (x + 1)`
   
   #### Example:
   For `x = 18` (binary `10010`):
   ```
   x + 1 = 19 (binary 10011)
   x | (x + 1) = 10010 | 10011 = 10011
   ```
   The result is `10011` (19 in decimal), where the rightmost `0` has been set to `1`.

3. **Get the Lowermost Set Bit**:
   - **What it does**: Isolates the rightmost `1`.
   - **How**: `x & -x`
   
   #### Example:
   For `x = 18` (binary `10010`):
   ```
   -x = -18 (in two's complement: 01110 + 1 = 01111)
   x & -x = 10010 & 01110 = 00010
   ```
   The result is `00010` (binary `2`), which isolates the rightmost `1`.

4. **Get the Index of the Lowermost Set Bit**:
   - **What it does**: Finds the position (index) of the rightmost `1`.
   - **How**: `(x & -x).bit_length() - 1`
   
   #### Example:
   For `x = 18` (binary `10010`):
   ```
   x & -x = 00010
   (x & -x).bit_length() = 2
   index = 2 - 1 = 1
   ```
   The result is `1`, meaning the rightmost `1` is at index `1` (starting from 0).

---

### Why We Need These Operations:
- **Efficiency**: Manipulating specific bits is much faster using these operations, which is crucial in performance-sensitive algorithms.
- **Applications**: Used in tasks like bit manipulation problems, generating subsets, and optimizing algorithms in low-level programming.

