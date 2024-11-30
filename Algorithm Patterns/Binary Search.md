### Binary Search

Binary Search is a method to efficiently search for a target value in a **sorted array**. Instead of checking each element one by one (like linear search), it cuts the search space in half at each step. This makes it super fast.

#### How It Works (Step-by-Step):
1. Start with two pointers: 
   - One at the **beginning** of the array (`low`).
   - One at the **end** of the array (`high`).

2. Find the **middle element** of the array:
   - `mid = (low + high) // 2`.

3. Compare the middle element with the target:
   - If it matches, you’ve found your target.
   - If the target is smaller, search the **left half** (move `high` to `mid - 1`).
   - If the target is larger, search the **right half** (move `low` to `mid + 1`).

4. Repeat until the pointers meet. If you can’t find the target, it’s not in the array.

---

### Binary Search Example

#### Code:
```python
def binary_search(nums, target):
    low, high = 0, len(nums) - 1

    while low <= high:
        mid = (low + high) // 2  # Find the middle element
        if nums[mid] == target:
            return mid  # Target found!
        elif nums[mid] < target:
            low = mid + 1  # Search the right half
        else:
            high = mid - 1  # Search the left half

    return -1  # Target not found
```

#### Input and Output:
```python
nums = [1, 3, 5, 7, 9, 11]
target = 7
print(binary_search(nums, target))  # Output: 3 (index of 7)
```
