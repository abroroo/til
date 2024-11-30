## Prefix Sum 

The prefix sum is a pattern where we **pre-calculate running totals or counts in a list**, so we can quickly answer questions like sums, counts, or patterns over a range of indices without recalculating everything every time.

- Instead of recalculating sums or counts repeatedly, we use a precomputed array where:
  - `prefix_sum[i]` represents the sum of elements from the start of the array up to index `i`.


#### **How Does It Work?**
1. **Precompute the Prefix Sum Array:**
   - At each position, store the sum of all elements from the start up to that position.
   - Example:
     ```
     Original Array: [2, 4, 1, 3]
     Prefix Sum:     [2, 6, 7, 10]
     ```
2. **Use the Prefix Sum to Answer Queries:**
   - To find the sum of elements from index `start` to `end`:
     ```python
     range_sum = prefix_sum[end] - prefix_sum[start - 1]
     ```
   - If `start = 0`, just use `prefix_sum[end]`.

---

#### **Implementation in Python**

```python
def compute_prefix_sum(arr):
    prefix_sum = [0] * len(arr) # Creates an array of length of arr with 0 values // Ex: [0,0,0,0,0]
    prefix_sum[0] = arr[0]  # First element stays the same

    for i in range(1, len(arr)):
        prefix_sum[i] = prefix_sum[i - 1] + arr[i]
    
    return prefix_sum


def range_sum_query(arr, start, end):
    prefix_sum = compute_prefix_sum(arr)
    
    if start == 0:
        return prefix_sum[end]
    else:
        return prefix_sum[end] - prefix_sum[start - 1]
```

**Example Usage:**
```python
arr = [2, 4, 1, 3]
print(compute_prefix_sum(arr))  # Output: [2, 6, 7, 10]

# Find sum from index 1 to 3
print(range_sum_query(arr, 1, 3))  # Output: 8 (4 + 1 + 3)
```

---

#### **When Should You Use Prefix Sum?**
Use the prefix sum pattern when:
1. **You have multiple range-based queries**:
   - Example: Find the sum of subarrays `[start, end]` repeatedly.
2. **You need to calculate cumulative counts**:
   - Example: Count occurrences of a specific condition across a range of indices.
3. **The problem hints at optimizing repetitive operations**:
   - When recalculating values for overlapping ranges feels inefficient.

#### **Common Coding Problem Scenarios**
1. **Subarray Sum Problems:**
   - Example: Find the sum of elements in multiple subarrays efficiently.
2. **Frequency or Count of Elements:**
   - Example: Count the number of `1`s in multiple ranges of a binary array.
3. **Range-based Modifications or Queries:**
   - Example: Calculate the total change in a range of values based on a set of operations.

### **Why is Prefix Sum Useful?**
It reduces the time complexity of range-based queries from **O(n)** to **O(1)** after an **O(n)** preprocessing step. This makes it highly efficient for problems involving repeated queries.
