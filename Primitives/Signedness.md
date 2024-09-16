### Signedness and Its Implications for Shifting:

- **Signed integers**: Can represent both positive and negative numbers (e.g., `-5`, `3`). The most significant bit (MSB) is the **sign bit**: `0` for positive and `1` for negative numbers (using two's complement).
- **Unsigned integers**: Only represent positive numbers (e.g., `0`, `5`), and all bits represent the magnitude.

### Shifting and Signedness:
1. **Left shift (`<<`)**: Works the same for both signed and unsigned integers, shifting bits to the left and filling with `0`s. It effectively multiplies by powers of 2.
   
   - No sign issues here.

2. **Right shift (`>>`)**:
   - **For signed integers**: The right shift may preserve the sign bit (arithmetic shift). If the number is negative, it fills with `1`s (MSB stays `1`).
   - **For unsigned integers**: It shifts right and fills with `0`s (logical shift).

### Example:

- **Signed `-8 >> 2`**: Fills with `1`s → `11111000(-8) >> 2 = 11111110` (remains negative, `-2`).
- **Unsigned `8 >> 2`**: Fills with `0`s → `00001000(8) >> 2 = 00000010` (`2` in decimal).

Signedness affects how the right shift behaves, especially for negative numbers.
