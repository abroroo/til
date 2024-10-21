# Merge Intervals Pattern 🧩

### What’s It About?
The **Merge Intervals Pattern** is all about squishing overlapping intervals together so that you end up with only **non-overlapping** ones. This is super helpful when you’re dealing with **time ranges** or any kind of data that has **start** and **end** points.

### Why is this useful?
Think of it like scheduling meetings. You have different meeting times, but some of them overlap. Instead of dealing with messy overlaps, you want to merge them into one clean time block. Once merged, you can see exactly when you’re free and when you’re busy—**no gaps or overlaps**.


### How to Approach It:

1. **Sort the intervals by their start value**.
   - Use Python’s `sort()` function with a custom key.
   - Example: `intervals.sort(key=lambda x: x[0])`
   - Sorting helps because we can easily compare each interval with the previous one.

2. **Set up initial values**:
   - Start by grabbing the first interval’s `start` and `end`.
   - Example:
     ```python
     start = intervals[0][0]
     end = intervals[0][1]
     ```

3. **Loop through the intervals**:
   - For each interval, check if it overlaps with the previous one:
     - If they overlap (`current_interval[0] <= end`), merge them by updating the `end` to the later end time (`max(end, current_interval[1])`).
     - If no overlap, add the previous interval to the result and start working with the new one.

4. **After the loop**, add the last interval to the result.

5. **Return your merged intervals**.

### Example Code:

```python
class Solution:
    def merge(self, intervals):
        if len(intervals) < 2:  # If there's only 1 or no intervals, just return it
            return intervals
        
        # Step 1: Sort the intervals by their start value
        intervals.sort(key=lambda x: x[0])

        merged_intervals = []
        start = intervals[0][0]  # Grab the first interval's start
        end = intervals[0][1]    # Grab the first interval's end

        # Step 2: Loop through the rest of the intervals
        for i in range(1, len(intervals)):
            current_interval = intervals[i]
            # If current interval overlaps with the last one, merge them
            if current_interval[0] <= end:
                end = max(end, current_interval[1])  # Extend the end if they overlap
            else:
                merged_intervals.append([start, end])  # No overlap, so add the last merged interval
                start = current_interval[0]  # Start a new interval
                end = current_interval[1]

        # Step 3: Don't forget to add the last interval
        merged_intervals.append([start, end])

        return merged_intervals

# Example Usage
intervals = [[1, 4], [2, 5], [7, 9]]
solution = Solution()
merged = solution.merge(intervals)
print("Merged intervals:", merged)  # Output: [[1, 5], [7, 9]]
```

### Why Sort by `start`?

Sorting is necessary because it makes it easy to compare intervals in order. Without sorting, we'd have a mess of intervals to compare, and it would be way harder to merge them.

- Sorting is done with:
  ```python
  intervals.sort(key=lambda x: x[0])
  ```
  - **What’s this `key=lambda` thing?** It’s just telling Python to sort based on the first value (`x[0]`) of each interval. So, for each interval like `[1, 4]`, Python looks at `1` to decide the order.

### Useful Slicing Tricks:
- **`[1:]`**: Skips the first item in a list and gives you the rest.
- **`[-1]`**: Refers to the last item in a list.

### Example of Merging:

For input intervals:
```python
intervals = [[1, 4], [2, 5], [7, 9]]
```
After merging, you get:
```python
Merged intervals: [[1, 5], [7, 9]]
```

### Complexity:
- **Time Complexity**: `O(n log n)` because of sorting, then `O(n)` for merging.
- **Space Complexity**: `O(n)` to store the merged intervals.

