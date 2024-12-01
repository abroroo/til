
### **`()` → Tuple**
- Immutable sequence of items.
- Example: `(1, 2, 3)`

#### Methods:
- **`count(x)`**: Returns the number of occurrences of `x` in the tuple.
- **`index(x)`**: Returns the index of the first occurrence of `x`.

#### Accessing Values:
1. **Indexing**:
   ```python
   my_tuple = (10, 20, 30)
   print(my_tuple[1])  # Output: 20
   ```
2. **Unpacking**:
   ```python
   my_tuple = (10, 20, 30)
   a, b, c = my_tuple
   print(b)  # Output: 20
   ```
3. **Iteration**:
   ```python
   my_tuple = (10, 20, 30)
   for value in my_tuple:
       print(value)  # Outputs: 10, 20, 30 (one per line)
   ```

---

### **`{}` → Dictionary**
- Key-value pairs.
- Example: `{'key': 'value', 'a': 1}`

#### Methods:
- **`clear()`**: Removes all items.
- **`copy()`**: Returns a shallow copy.
- **`fromkeys(iterable, value=None)`**: Creates a new dictionary with keys from an iterable and values set to `value`.
- **`get(key, default=None)`**: Returns the value for `key`, or `default` if `key` is not found.
- **`items()`**: Returns a view of key-value pairs as tuples.
- **`keys()`**: Returns a view of dictionary keys.
- **`pop(key, default=None)`**: Removes the item with `key` and returns its value, or `default` if `key` is not found.
- **`popitem()`**: Removes and returns an arbitrary key-value pair (LIFO from Python 3.7+).
- **`setdefault(key, default=None)`**: Returns the value of `key`, or inserts `key` with `default` if `key` is not present.
- **`update([other])`**: Updates the dictionary with key-value pairs from another dictionary or iterable.
- **`values()`**: Returns a view of dictionary values.

#### Accessing Values:
1. **Using Keys**:
   ```python
   my_dict = {'a': 1, 'b': 2}
   print(my_dict['a'])  # Output: 1
   ```
2. **Using `get()`**:
   ```python
   print(my_dict.get('b', 0))  # Output: 2
   print(my_dict.get('c', 0))  # Output: 0 (default)
   ```
3. **Iteration**:
   ```python
   for key, value in my_dict.items():
       print(f"{key}: {value}")  # Output: a: 1, b: 2
   ```

---

### **`[]` → List**
- Mutable sequence of items.
- Example: `[1, 2, 3]`

#### Methods:
- **`append(x)`**: Adds an item to the end.
- **`clear()`**: Removes all items.
- **`copy()`**: Returns a shallow copy.
- **`count(x)`**: Returns the number of occurrences of `x`.
- **`extend(iterable)`**: Extends the list by appending elements from the iterable.
- **`index(x, start=0, end=len(list))`**: Returns the index of the first occurrence of `x`.
- **`insert(i, x)`**: Inserts `x` at position `i`.
- **`pop([i])`**: Removes and returns the item at position `i` (last item if `i` is omitted).
- **`remove(x)`**: Removes the first occurrence of `x`.
- **`reverse()`**: Reverses the list in place.
- **`sort(key=None, reverse=False)`**: Sorts the list in ascending order (can be customized with `key` or `reverse`).

#### Accessing Values:
1. **Indexing**:
   ```python
   my_list = [10, 20, 30]
   print(my_list[1])  # Output: 20
   ```
2. **Slicing**:
   ```python
   print(my_list[1:])  # Output: [20, 30]
   ```
3. **Iteration**:
   ```python
   for value in my_list:
       print(value)  # Outputs: 10, 20, 30 (one per line)
   ``` 





---







**`class` → use class to create an Object (Internally Dictionary)**  
- Classes are blueprints for objects. Instances use a dictionary (`__dict__`) to store attributes.  
- Example:  
  ```python
  class MyClass:
      def __init__(self, name):
          self.name = name
  obj = MyClass("example")
  print(obj.__dict__)  # {'name': 'example'}
  ```

**Hash Map → Dictionary**  
- A Python `dict` behaves as a hash map, using hashed keys to store key-value pairs.  
- Example: `hash_map = {'key': 'value'}`

**Array → List**  
- Python's `list` is used for array-like functionality.  
- Example: `[1, 2, 3, 4]`
