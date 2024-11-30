##  K-Way Merge 

The **K-Way Merge Pattern** is used when we need to combine multiple sorted lists (or arrays) into one big sorted list. Instead of merging them one by one (which can be slow), this pattern uses efficient techniques to merge all the lists simultaneously.


#### What Does "K-Way" Mean?

The "K" in K-Way Merge refers to the **number of sorted lists** we are merging. For example:
- If we have 3 sorted lists, it’s a **3-way merge**.
- If we have 10 sorted lists, it’s a **10-way merge**.


#### Why Do We Use K-Way Merge?

When working with sorted lists (like in sorting algorithms or file processing), merging them efficiently is key. The K-Way Merge Pattern helps us do this in **logarithmic time**, making it ideal for large datasets.

1. Use a **min-heap** (or manual sorting logic) to keep track of the smallest elements from each list.
2. Repeatedly extract the smallest element and add it to the final list.
3. Replace the extracted element with the next one from the same list, ensuring the heap (or sorted order) is maintained.

---

### Example Problem: Merge K Sorted Lists

#### Problem:
You’re given 3 sorted lists:
```
list1 = [1, 4, 7]
list2 = [2, 5, 8]
list3 = [3, 6, 9]
```

Merge them into a single sorted list:
```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```


#### Approach:
We keep track of the smallest elements from all lists:
1. Start by looking at the **first element of each list**.
2. Add the smallest one to the final list.
3. Move to the next element in the list where the smallest came from.
4. Repeat until all lists are fully merged.

---

#### Code:
```python
def merge_k_sorted_lists(lists):
    # Step 1: Flatten the lists into a single list
    all_elements = []
    for lst in lists:
        all_elements.extend(lst)

    # Step 2: Sort the combined list
    all_elements.sort()

    return all_elements

# Example usage
list1 = [1, 4, 7]
list2 = [2, 5, 8]
list3 = [3, 6, 9]

result = merge_k_sorted_lists([list1, list2, list3])
print("Merged list:", result)
```

1. **Flatten** all lists into a single list:
   ```
   list1 + list2 + list3 = [1, 4, 7, 2, 5, 8, 3, 6, 9]
   ```
2. **Sort** the combined list:
   ```
   [1, 2, 3, 4, 5, 6, 7, 8, 9]
   ```

---

### A More Efficient Approach (Simulating a Min-Heap)

Instead of sorting everything upfront, we can merge incrementally. This method keeps track of the **current smallest element** from each list using manual comparisons.

#### Code:
```python
def merge_k_sorted_lists_efficient(lists):
    # Step 1: Track the current index for each list
    pointers = [0] * len(lists)
    merged_list = []

    while True:
        smallest = float('inf')
        smallest_list_index = -1

        # Step 2: Find the smallest current element among the lists
        for i in range(len(lists)):
            if pointers[i] < len(lists[i]) and lists[i][pointers[i]] < smallest:
                smallest = lists[i][pointers[i]]
                smallest_list_index = i

        # If we couldn't find a smallest element, we're done
        if smallest_list_index == -1:
            break

        # Step 3: Add the smallest element to the merged list
        merged_list.append(smallest)

        # Step 4: Move the pointer in the list we took the smallest element from
        pointers[smallest_list_index] += 1

    return merged_list

# Example usage
list1 = [1, 4, 7]
list2 = [2, 5, 8]
list3 = [3, 6, 9]

result = merge_k_sorted_lists_efficient([list1, list2, list3])
print("Merged list:", result)
```

#### How It Works:
1. **Track Current Positions**: Use a `pointers` array to keep track of where we are in each list.
2. **Compare Smallest Elements**: Look at the current elements from all lists and pick the smallest.
3. **Move Pointer**: Move forward in the list where we picked the smallest element.
4. **Repeat** until all lists are fully merged.


#### Output:
For `[1, 4, 7], [2, 5, 8], [3, 6, 9]`:
```
Merged list: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

### Real-Life Example:
Imagine combining search results from multiple search engines. Each engine gives a sorted list of results, and you want one combined sorted list.
