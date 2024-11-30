## Modified Binary Search

Modified Binary Search is when we **tweak the standard [Binary Search](https://github.com/abroroo/til/tree/main/Algorithm%20Patterns)** to solve more complex problems. Instead of just searching for a single number, we can adjust it for special cases like rotations, duplicates, or conditions.

#### 1. **Find the First or Last Occurrence**
If a number appears multiple times, we might need its first or last index.

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

We’ll use it when:
1. We need efficient solutions for **sorted or rotated arrays**.
2. Problems involve finding specific conditions, like the first/last occurrence or a pivot point.
