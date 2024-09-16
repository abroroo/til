
In binary there is a pattern called **mask** which basically is a binary number with zeros(0) all over and one(1) at specific index(position) you want. 

Basically, a **mask** acts like a "pointer" to a specific bit (or bits) in a binary number. It allows you to target and manipulate that bit without affecting the others.

### How It Works:
- The mask is a binary number where certain bits are set to `1` (which "points" to the specific bits you're interested in).
- You can then use bitwise operations to:
  - **Check** (AND `&`) if the bit at that index is set.
  - **Set** (OR `|`) a bit to `1`.
  - **Clear** (AND `& ~`) a bit to `0`.
  - **Toggle** (XOR `^`) a bit (flip its value).

### Example:
If you have a number `x = 1011` (binary), and you want to manipulate the 2nd bit (from the right):
```python
mask = 1 << 1  # This creates a mask like 0010

# To check the 2nd bit:
check = x & mask  # Results in 0010 if the 2nd bit is set

# To set the 2nd bit:
x = x | mask  # Forces the 2nd bit to 1

# To clear the 2nd bit:
x = x & ~mask  # Forces the 2nd bit to 0

# To toggle the 2nd bit:
x = x ^ mask  # Flips the 2nd bit
```

So, the mask "points" to the bit you want to work with!
