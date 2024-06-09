# Data Structure


### O(1) - Constant Time

This example demonstrates accessing an element in a list.

```python
def get_first_element(lst):
    return lst[0]  # This operation takes constant time regardless of the list size.

# Example usage:
print(get_first_element([1, 2, 3, 4, 5]))  # Output: 1
```

### O(log n) - Logarithmic Time

This example demonstrates a binary search in a sorted array.

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Example usage:
print(binary_search([1, 2, 3, 4, 5], 4))  # Output: 3 (index of 4 in the array)
```

### O(n) - Linear Time

This example demonstrates finding the maximum element in an array.

```python
def find_maximum(arr):
    max_element = arr[0]
    for num in arr:
        if num > max_element:
            max_element = num
    return max_element

# Example usage:
print(find_maximum([1, 2, 3, 4, 5]))  # Output: 5
```

### O(n log n) - Linearithmic Time

This example demonstrates Merge Sort, a sorting algorithm.

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        merge_sort(left_half)
        merge_sort(right_half)

        i = j = k = 0
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1

# Example usage:
arr = [5, 2, 3, 1, 4]
merge_sort(arr)
print(arr)  # Output: [1, 2, 3, 4, 5]
```

### O(n^2) - Quadratic Time

This example demonstrates Bubble Sort, a simple sorting algorithm.

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

# Example usage:
arr = [5, 2, 3, 1, 4]
bubble_sort(arr)
print(arr)  # Output: [1, 2, 3, 4, 5]
```

### O(2^n) - Exponential Time

This example demonstrates calculating the n-th Fibonacci number using a naive recursive method.

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# Example usage:
print(fibonacci(5))  # Output: 5 (the 5th Fibonacci number)
```

## In Swift, the complexity of operations on arrays and dictionaries varies depending on the specific operation being performed. Below are the most common operations along with their time complexities:

### Array

1. **Access Element by Index**
   - **Time Complexity:** O(1)
   - **Explanation:** Direct access to elements by index is a constant-time operation.

   ```swift
   let array = [1, 2, 3, 4, 5]
   let element = array[2]  // O(1)
   ```

2. **Append Element**
   - **Time Complexity:** Amortized O(1)
   - **Explanation:** Append operations are generally O(1) due to potential allocation of space. When an array needs to allocate more space, the operation can take longer, thus the amortized time complexity is considered.

   ```swift
   var array = [1, 2, 3]
   array.append(4)  // Amortized O(1)
   ```

3. **Insert Element**
   - **Time Complexity:** O(n)
   - **Explanation:** Insertion into the middle of an array may require shifting elements, which takes linear time.

   ```swift
   var array = [1, 2, 3]
   array.insert(4, at: 1)  // O(n)
   ```

4. **Remove Element**
   - **Time Complexity:** O(n)
   - **Explanation:** Removing an element requires shifting elements to close the gap, which is a linear operation.

   ```swift
   var array = [1, 2, 3, 4]
   array.remove(at: 2)  // O(n)
   ```

5. **Search for Element (Linear Search)**
   - **Time Complexity:** O(n)
   - **Explanation:** Searching requires checking each element one by one in the worst case.

   ```swift
   let array = [1, 2, 3, 4, 5]
   let index = array.firstIndex(of: 3)  // O(n)
   ```

### Dictionary (Hash Table)

1. **Access/Modify Value for Key**
   - **Time Complexity:** Amortized O(1)
   - **Explanation:** Accessing or modifying a value by its key is generally a constant-time operation due to the underlying hash table.

   ```swift
   var dictionary = ["a": 1, "b": 2, "c": 3]
   let value = dictionary["b"]  // Amortized O(1)
   dictionary["b"] = 4  // Amortized O(1)
   ```

2. **Insert Key-Value Pair**
   - **Time Complexity:** Amortized O(1)
   - **Explanation:** Inserting a new key-value pair is generally a constant-time operation. However, the hash table might need to be resized, which makes the complexity amortized.

   ```swift
   var dictionary = ["a": 1]
   dictionary["b"] = 2  // Amortized O(1)
   ```

3. **Remove Key-Value Pair**
   - **Time Complexity:** Amortized O(1)
   - **Explanation:** Removing a key-value pair is generally a constant-time operation.

   ```swift
   var dictionary = ["a": 1, "b": 2, "c": 3]
   dictionary.removeValue(forKey: "b")  // Amortized O(1)
   ```

4. **Check if Key Exists**
   - **Time Complexity:** Amortized O(1)
   - **Explanation:** Checking for the existence of a key is generally a constant-time operation.

   ```swift
   let dictionary = ["a": 1, "b": 2]
   let exists = dictionary.keys.contains("a")  // Amortized O(1)
   ```

These complexities assume that the underlying data structures are implemented efficiently and take average cases into account. In the worst case, due to hash collisions, dictionary operations could degrade to O(n), but this is rare with a good hash function.


