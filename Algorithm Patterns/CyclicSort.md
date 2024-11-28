### Cyclic Sort

Cyclic Sort is a in-place sorting method for arrays where the numbers fall within a specific range, like `0` to `n` or `1` to `n`. It runs in `O(n)` time and doesn’t need extra space.

**How It Works**:
1. Start from the first index.
2. For each number, put it in its correct spot:
   - If the number isn’t at the right index, swap it with the element at its target index.
   - If it’s in the right spot or is a duplicate, just move to the next number.
3. Repeat until the whole array is sorted.

![image](https://github.com/user-attachments/assets/e95edea6-f2bb-4ec5-a9fd-3626ff0478e5)

**Code**:
```python
def cyclic_sort(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i] - 1  # or nums[i] for 0-based arrays

      # swap conditon for 0 to n  
         # ex: if nums[i] != nums[correct_index] and nums[i] < len(nums)

        if nums[i] != nums[correct_index]:  # swap condition for range 1 to n
            nums[i], nums[correct_index] = nums[correct_index], nums[i]  # Swap if not in the right spot
        else:
            i += 1  # Move on if it's correct
    return nums
```

**Example Walkthrough**:
Sort `[3, 1, 5, 4, 2]`:

| Step | Array State   | Action                        |
|------|---------------|--------------------------------|
| 1    | `[3, 1, 5, 4, 2]` | Swap 3 with 5 at index 2      |
| 2    | `[5, 1, 3, 4, 2]` | Swap 5 with 2 at index 4      |
| 3    | `[2, 1, 3, 4, 5]` | Swap 2 with 1 at index 1      |
| 4    | `[1, 2, 3, 4, 5]` | Numbers in correct places, done! |

**Uses**:
- Finding missing or duplicate numbers.
- Sorting arrays with a limited range.

**Quick Tip**:
Add a boundary check (`nums[i] < len(nums)`) if the range starts at `0` to avoid index errors when `nums[i]` equals `n`.

