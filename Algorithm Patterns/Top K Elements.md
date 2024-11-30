## Top K Elements

The **Top K Elements Pattern** is a method to find the **K largest, smallest, or most frequent elements** in a dataset. It’s efficient because we focus on only part of the dataset rather than sorting everything.

#### What Does "Top K" Mean?

Think of "Top K" as solving problems like:
- Finding the **3 largest numbers** in a list.
- Finding the **2 most frequent words** in a paragraph.

This pattern saves time by avoiding sorting the entire dataset when we only care about K elements.


#### What Is a Heap?

A **Heap** is a special data structure used to manage "Top K" elements:
- A **Min-Heap** keeps the smallest element at the top.
- A **Max-Heap** keeps the largest element at the top.
  
In Python, heaps are just **lists**, and we can manage them with basic operations:
- Add elements with `append()`.
- Maintain heap order manually by comparing parent and child nodes.

---

### Example 1: Find the Top K Largest Numbers

#### Problem:
Find the **3 largest numbers** in `[1, 5, 12, 2, 11, 5]`.

#### Approach:
1. Use a **list as a min-heap**.
2. Add elements to the list one by one.
3. If the list grows larger than `K`, remove the smallest element (manually find it).

#### Code:
```python
def find_k_largest(nums, k):
    min_heap = []  # List to act as a min-heap

    for num in nums:
        min_heap.append(num)  # Add the number to the heap
        # If the heap has more than K elements, remove the smallest one
        if len(min_heap) > k:
            min_heap.remove(min(min_heap))  # Remove the smallest element manually

    return min_heap  # The heap now contains the top K largest elements

# Example usage
nums = [1, 5, 12, 2, 11, 5]
k = 3
print(find_k_largest(nums, k))  # Output: [11, 12, 5] (not necessarily sorted)
```

---

### Example 2: Find the Top K Most Frequent Elements

#### Problem:
Find the **2 most frequent elements** in `[1, 1, 1, 2, 2, 3]`.

#### Approach:
1. Use a dictionary to count frequencies of each element.
2. Use a **list as a min-heap** to store the top K elements.
3. For every element in the frequency dictionary:
   - Add it to the heap.
   - If the heap size exceeds K, remove the element with the smallest frequency.

#### Code:
```python
def find_k_frequent(nums, k):
    # Step 1: Count frequencies
    freq_map = {}
    for num in nums:
        freq_map[num] = freq_map.get(num, 0) + 1  # Increment count
    
    min_heap = []  # List to act as a min-heap

    # Step 2: Process each frequency
    for num, freq in freq_map.items():
        min_heap.append((freq, num))  # Add (frequency, number) to the heap
        if len(min_heap) > k:
            # Remove the element with the smallest frequency
            min_heap.remove(min(min_heap, key=lambda x: x[0]))

    # Extract only the numbers from the heap
    return [num for freq, num in min_heap]

# Example usage
nums = [1, 1, 1, 2, 2, 3]
k = 2
print(find_k_frequent(nums, k))  # Output: [2, 1]
```

### Key Operations Without Libraries:
1. **Adding an Element**: Use `list.append()`.
2. **Finding the Smallest or Largest**: Use `min()` or `max()`.
3. **Removing the Smallest or Largest**: Use `.remove()` after finding it manually.


---

### Real-Life Example
Imagine you're running a quiz competition:
- You need the **top 5 scores**.
- Instead of sorting the scores of 1,000 participants, you can use a min-heap to keep track of only the top 5 efficiently.


