### Two Sum Problem

#### Problem Statement
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to the target. You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Example
```python
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

### Approaches

#### 1. **Brute Force**
- **Approach**: Use two nested loops to iterate through the array. For each pair of elements, check if their sum equals the target.
- **Complexity**:
  - **Time Complexity**: \(O(n^2)\) due to the nested loops.
  - **Space Complexity**: \(O(1)\) as no additional data structures are used.
- **Implementation**:
  ```python
  def two_sum(nums, target):
      for i in range(len(nums)):
          for j in range(i + 1, len(nums)):
              if nums[i] + nums[j] == target:
                  return [i, j]
  ```

#### 2. **Two-pass Hash Table**
- **Approach**: In the first pass, create a hash table to store each element's value and its index. In the second pass, for each element, check if the complement (target - current element) exists in the hash table.
- **Complexity**:
  - **Time Complexity**: \(O(n)\) because we traverse the list twice.
  - **Space Complexity**: \(O(n)\) to store elements in the hash table.
- **Implementation**:
  ```python
  def two_sum(nums, target):
      hash_table = {}
      for i in range(len(nums)):
          hash_table[nums[i]] = i
      for i in range(len(nums)):
          complement = target - nums[i]
          if complement in hash_table and hash_table[complement] != i:
              return [i, hash_table[complement]]
  ```

#### 3. **One-pass Hash Table**
- **Approach**: While traversing the array, for each element, check if its complement (target - current element) already exists in the hash table. If it does, return the indices. Otherwise, add the element to the hash table.
- **Complexity**:
  - **Time Complexity**: \(O(n)\) as we traverse the list once.
  - **Space Complexity**: \(O(n)\) to store elements in the hash table.
- **Implementation**:
  ```python
  def two_sum(nums, target):
      hash_table = {}
      for i, num in enumerate(nums):
          complement = target - num
          if complement in hash_table:
              return [hash_table[complement], i]
          hash_table[num] = i
  ```

  You're right! The two-pointer technique is another efficient approach to solve the Two Sum problem, but it typically applies when the array is sorted. Here's how you can use the two-pointer approach for the Two Sum problem:

#### 4. **Two-pointer Approach**

#### Approach
1. **Sort the Array**: First, sort the array while keeping track of the original indices.
2. **Initialize Two Pointers**: Use two pointers, one starting at the beginning (`left`) and the other at the end (`right`) of the sorted array.
3. **Move Pointers Based on Sum**: Calculate the sum of the elements at the two pointers:
   - If the sum equals the target, return the indices of the two elements.
   - If the sum is less than the target, move the left pointer to the right to increase the sum.
   - If the sum is greater than the target, move the right pointer to the left to decrease the sum.

#### Complexity
- **Time Complexity**: \(O(n \log n)\) due to the sorting step.
- **Space Complexity**: \(O(n)\) for storing the original indices.

#### Implementation

Here’s a detailed implementation of the two-pointer approach:

```python
def two_sum(nums, target):
    # Create a list of tuples (value, index)
    nums_with_index = [(num, i) for i, num in enumerate(nums)]
    
    # Sort the list by values
    nums_with_index.sort(key=lambda x: x[0])
    
    # Initialize two pointers
    left = 0
    right = len(nums_with_index) - 1
    
    # Iterate until the pointers meet
    while left < right:
        current_sum = nums_with_index[left][0] + nums_with_index[right][0]
        
        if current_sum == target:
            # Return the original indices of the two numbers
            return [nums_with_index[left][1], nums_with_index[right][1]]
        elif current_sum < target:
            # Move the left pointer to the right
            left += 1
        else:
            # Move the right pointer to the left
            right -= 1
    
    # If no solution is found (although the problem guarantees one)
    return []

# Example usage
nums = [2, 7, 11, 15]
target = 9
print(two_sum(nums, target))  # Output: [0, 1]
```

### Detailed Explanation

1. **Sorting the Array**: 
   - First, we create a list of tuples where each tuple contains the element and its original index.
   - We then sort this list based on the values of the elements. This helps in efficiently finding the pair using two pointers.

2. **Initializing Two Pointers**: 
   - The `left` pointer starts at the beginning (index 0) and the `right` pointer starts at the end (last index) of the sorted list.

3. **Iterating with Two Pointers**:
   - In each iteration, we calculate the sum of the elements at the `left` and `right` pointers.
   - If the sum equals the target, we return the original indices of these two elements.
   - If the sum is less than the target, we move the `left` pointer to the right to increase the sum.
   - If the sum is greater than the target, we move the `right` pointer to the left to decrease the sum.

4. **Returning the Result**:
   - The loop continues until the two pointers meet. If a pair is found that sums to the target, the indices are returned.
   - The problem guarantees exactly one solution, so this method will always find the pair if implemented correctly.

### Advantages and Use Cases

- **Efficiency**: This method is efficient in terms of time complexity after sorting the array, especially for large datasets.
- **Simplicity**: The logic of moving two pointers based on the comparison with the target sum is straightforward and easy to understand.
- **Sorted Data**: This approach is particularly useful when the array is already sorted or when sorting is feasible within the problem constraints.

### Detailed Explanation of the One-pass Hash Table Approach

1. **Initialize a Hash Table**: Create an empty dictionary (`hash_table`) to store the elements and their indices.

2. **Traverse the Array**: Loop through each element (`num`) in the array along with its index (`i`).

3. **Check for Complement**: For each element, calculate its complement (`target - num`).
   - **If the complement is in the hash table**: It means we have already seen the other number that, together with the current number, sums up to the target. In this case, return the indices of the complement and the current element.
   - **If the complement is not in the hash table**: Add the current element and its index to the hash table.

4. **Return the Result**: The function returns the indices of the two numbers that add up to the target.

This approach ensures that each element is processed only once, making it the most efficient solution among the discussed approaches.

### Example Walkthrough

Consider `nums = [2, 7, 11, 15]` and `target = 9`:

- **Step 1**: Initialize `hash_table = {}`.
- **Step 2**: Start loop:
  - **Iteration 1**: `i = 0`, `num = 2`, `complement = 9 - 2 = 7`.
    - `7` is not in `hash_table`.
    - Add `2` to `hash_table`: `hash_table = {2: 0}`.
  - **Iteration 2**: `i = 1`, `num = 7`, `complement = 9 - 7 = 2`.
    - `2` is in `hash_table` with index `0`.
    - Return `[0, 1]`. 

This walkthrough illustrates how the algorithm efficiently finds the solution in a single pass through the array.
