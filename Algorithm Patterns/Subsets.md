## Subsets

Imagine we have a small group of items, like `[1, 5, 3]`, and we want to figure out all the different combinations we can make with them. The **Subsets Pattern** is a method to do this systematically and easily.

### What Are Subsets?
A **subset** is just a smaller collection of elements from a set. It can have:
- None of the elements (empty subset: `[]`).
- Some of the elements (`[1]`, `[5]`, `[1, 5]`).
- All the elements (`[1, 5, 3]`).

For `[1, 5, 3]`, the subsets are:
```
[[], [1], [5], [1, 5], [3], [1, 3], [5, 3], [1, 5, 3]]
```


### How Do We Find Subsets?
We build them step by step, like this:

1. **Start with an empty subset**: `[]`
2. **Add one number at a time** to all the subsets we already have:
   - Add `1`: `[[], [1]]`
   - Add `5`: `[[], [1], [5], [1, 5]]`
   - Add `3`: `[[], [1], [5], [1, 5], [3], [1, 3], [5, 3], [1, 5, 3]]`

---

### Python Code for Subsets
Here’s how we can write this process in Python:

```python
def find_subsets(nums):
    # Start with an empty subset
    subsets = [[]]
    
    # Loop through each number
    for num in nums:
        new_subsets = []  # Temporary storage for new subsets
        for current in subsets:
            # Add the current number to each subset
            new_subsets.append(current + [num])
        # Add all new subsets to the main list
        subsets.extend(new_subsets)
    
    return subsets

# Example usage
nums = [1, 5, 3]
result = find_subsets(nums)
print("All subsets:")
print(result)
```

---

### Why Is the Subsets Pattern Useful?
We’ll use this pattern in problems that:
- Ask for all combinations of a set (like a shopping list or team selections).
- Mention **subsets**, **power sets**, or **combinations** in the problem description.



### Real-Life Example
Imagine planning outfits with:
- A shirt (`1`), pants (`5`), and a hat (`3`).

All combinations of these items:
- No items: `[]`
- Just a shirt: `[1]`
- Shirt and pants: `[1, 5]`
- Shirt, pants, and hat: `[1, 5, 3]`
- ...and so on!


