**Parity** refers to whether the number of `1`s in a binary number (or binary "word") is **even** or **odd**.

### Types of Parity:
1. **Even Parity**: If the number of `1`s in the binary word is even, it has even parity.
2. **Odd Parity**: If the number of `1`s in the binary word is odd, it has odd parity.

### Example:
- **Binary word**: `10110101`
  - Number of `1`s: 5 → **Odd parity**.
  
- **Binary word**: `11110000`
  - Number of `1`s: 4 → **Even parity**.

### Purpose:
- **Error detection**: Parity is often used in data transmission to detect errors. A parity bit can be added to ensure the total number of `1`s is either even or odd, helping verify data integrity.

### Parity Calculation:
To calculate the parity of a binary number, you can XOR all the bits together. If the result is `0`, it has even parity; if the result is `1`, it has odd parity.
