### Two Pointers Pattern (For Sorted Lists)

- A **technique** where you use **two pointers** to work on a problem by starting at **different positions** in a sorted array (or list).
- Typically:
  - **One pointer starts at the beginning** of the list.
  - **The other pointer starts at the end**, and they "move" toward each other based on the logic.

---

#### Visualization:
Imagine you’re searching for two numbers in a sorted list that add up to a target sum:

```plaintext
List: [1, 2, 3, 4, 5, 6, 7]
       ^                 ^
     (left)           (right)

- Left pointer starts at 1.
- Right pointer starts at 7.
```

1. Check if the sum of `left` and `right` equals the target.
2. If the sum is **too small**, move the left pointer forward to increase it.
3. If the sum is **too big**, move the right pointer backward to decrease it.

---

#### When Is It Useful?
1. **Finding Pairs**:
   - Locate pairs in a sorted list that satisfy a condition (e.g., sum to a target).
2. **Sorting Problems**:
   - Solve problems involving merging, comparing, or rearranging elements in sorted arrays.
3. **Duplicates/Unique Checks**:
   - Efficiently skip over duplicates in a sorted list.

---

#### Basic Implementation in Python

**1. Finding Two Numbers with Target Sum:**
```python
def two_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1  # Start pointers at both ends
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:  # Found the pair
            return [arr[left], arr[right]]
        elif current_sum < target:  # Move left pointer to increase sum
            left += 1
        else:  # Move right pointer to decrease sum
            right -= 1
    return []  # No pair found
```

Example usage:
```python
arr = [1, 2, 3, 4, 6]
target = 6
print(two_sum_sorted(arr, target))  # Output: [2, 4]
```

---

#### Why It Works:
- Sorted lists make it efficient:
  - Move the **left pointer** forward to increase the sum.
  - Move the **right pointer** backward to decrease the sum.
- Avoids unnecessary iterations through the list, achieving an **O(n)** time complexity.

