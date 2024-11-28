### Sliding Window 

- This is a **handy trick** for solving problems with **subarrays** or **substrings** in things like arrays or strings.
- The idea: We keep a **"window" of elements** (a part of the data) and **slide** it along while adjusting the window size or contents as needed.

Picture it like this:

```plaintext
Array: [1, 3, 2, 5, 1, 1, 2, 3]
Window size: 3
         [1, 3, 2] -> Slide -> [3, 2, 5] -> Slide -> [2, 5, 1]
```

The window moves one step at a time, and we work only on the part inside the window. It’s like scanning the array without having to start over every time.

![image](https://github.com/user-attachments/assets/7a551319-c6f9-4043-a843-0152f46d4075)

---

#### When Do We Use It?
1. **Fixed Window Size**:
   - Example: Finding the maximum sum of a subarray of a fixed size.
2. **Changing Window Size**:
   - Example: Finding the smallest subarray that meets a condition (like a sum greater than a target).
3. **Cutting Down Repetition**:
   - Works great when we don’t want to reprocess parts of the array that are still useful.

---

#### Basic Implementation in Python

**1. Maximum Sum of Subarray of Size `k`:**
Let’s say we want the biggest sum of any 3 numbers in a row.

```python
def max_sum_subarray(arr, k):
    max_sum = 0
    window_sum = 0
    start = 0

    for end in range(len(arr)):
        window_sum += arr[end]  # Add the new number to the window

        if end >= k - 1:  # When the window hits size k
            max_sum = max(max_sum, window_sum)  # Check the max sum
            window_sum -= arr[start]  # Remove the first number in the window
            start += 1  # Slide the window forward

    return max_sum
```

Example:
```python
arr = [1, 3, 2, 5, 1, 1, 2, 3]
k = 3
print(max_sum_subarray(arr, k))  # Output: 10 (from [3, 2, 5])
```

---

**2. Smallest Subarray with a Sum Greater Than a Target:**
Let’s shrink the window if it gets too big but still meets the goal.

```python
def min_subarray_sum(arr, target):
    start = 0
    window_sum = 0
    min_length = float('inf')

    for end in range(len(arr)):
        window_sum += arr[end]  # Add the new number to the window

        while window_sum >= target:  # Shrink if the sum is too big
            min_length = min(min_length, end - start + 1)
            window_sum -= arr[start]
            start += 1  # Slide the window forward

    return min_length if min_length != float('inf') else 0
```

Example:
```python
arr = [4, 2, 2, 7, 8, 1, 2, 8, 10]
target = 15
print(min_subarray_sum(arr, target))  # Output: 2 (from [8, 10])
```

---

#### Why It Works:
Sliding the window is smart because we don’t redo work. Instead of recalculating everything, we just adjust the window:
- Add one number.
- Remove one number.
- Boom, done!

This makes it fast and clean, usually **O(n)**, and perfect for problems where we want something like "biggest," "smallest," or "specific conditions" on subarrays or substrings.
