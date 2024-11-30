### Beginner-Friendly Note on Modified Binary Search

### What is Binary Search?

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


### What is Modified Binary Search?

Modified Binary Search is when we **tweak the standard Binary Search** to solve more complex problems. Instead of just searching for a single number, we can adjust it for different tasks.

---

### Examples of Modified Binary Search

#### 1. **Find the First or Last Occurrence**
If a number appears multiple times, you might need its first or last index.

#### Key Idea:
- Instead of returning as soon as the target is found, adjust `low` or `high` to keep searching the required half.

#### Code:
```python
def find_first(nums, target):
    low, high = 0, len(nums) - 1
    result = -1

    while low <= high:
        mid = (low + high) // 2
        if nums[mid] == target:
            result = mid  # Update result and keep searching left
            high = mid - 1
        elif nums[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return result
```


#### 2. **Find the Smallest Element in a Rotated Sorted Array**
Imagine a sorted array that’s been "rotated," like `[4, 5, 6, 7, 0, 1, 2]`. We need to find the smallest element.

#### Key Idea:
- Use Binary Search to find the point where the rotation happens.

#### Code:
```python
def find_min(nums):
    low, high = 0, len(nums) - 1

    while low < high:
        mid = (low + high) // 2
        if nums[mid] > nums[high]:  # Min is in the right half
            low = mid + 1
        else:  # Min is in the left half
            high = mid

    return nums[low]  # `low` will point to the smallest element
```

#### Input and Output:
```python
nums = [4, 5, 6, 7, 0, 1, 2]
print(find_min(nums))  # Output: 0
```


### Why Use Modified Binary Search?

You’ll use it when:
1. You need efficient solutions for **sorted or rotated arrays**.
2. Problems involve finding specific conditions, like the first/last occurrence or a pivot point.
