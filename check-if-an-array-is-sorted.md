# Problem : Check If An Array Is Sorted
---
## Problem Link : [Check if an Array is Sorted - GeeksforGeeks](https://www.geeksforgeeks.org/problems/check-if-an-array-is-sorted0701/1)
---
## Difficulty Level : 

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

---
# Statement 
Given an array of integers, determine whether the array is sorted in non-decreasing order (each element is less than or equal to the next). Return `True` if the array is sorted, otherwise return `False`.

**Example:**
```python
arr = [1, 2, 2, 4, 5]
# Output: True

arr = [5, 3, 2, 1]
# Output: False
```

**Constraints:**
* The array can contain any integers (positive, negative, or zero).
* The array may be empty or contain only one element (these are considered sorted).

**Summary:**
* Check if every element is less than or equal to the next.
* Return True if sorted, False otherwise.
* Works for any integer array.


---
# Optimized Approach
---

### Intuition
1. Iterate through the array from the second element to the end.
2. Compare each element with the previous one.
3. If any previous element is greater than the current, the array is not sorted.
4. Use a flag to track the result and break early if unsorted.

✅ **Key Idea:**
- Only one pass through the array is needed.
- Early exit as soon as unsorted order is found.

---
### Pseudocode
1. Initialize a flag variable.
2. For each index from 1 to end of array:
    - If previous element > current element:
        - Set flag to False and break.
3. If loop completes without breaking, set flag to True.
4. Return flag.

---
### Code
```python
    def isSorted(arr):
        flag = None
        for i in range(1, len(arr)):
            if arr[i-1] > arr[i]:
                flag = False
                break
        else:
            flag = True
        return flag
```
---
### Explanation
Use Chain of Thought:
1. Start with a flag variable to track if the array is sorted.
2. Loop from the second element to the end.
3. For each element, compare it with the previous one.
4. If any previous element is greater than the current, set flag to False and exit the loop early.
5. If the loop completes without finding any violations, set flag to True (array is sorted).
6. Return the flag value.

This approach ensures that the function stops checking as soon as it finds the array is not sorted, making it efficient.

---
### Time and Space Complexity
#### **Time Complexity** ![O(n)](https://img.shields.io/badge/Time%20Complexity-O(n)-blue)
1. Only one pass through the array (n-1 comparisons).
2. Early exit if unsorted order is found.

#### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only a flag variable and loop index are used.

### **Summary**
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)
---
# Edge Cases
- Empty array: considered sorted (returns True).
- Single element array: considered sorted (returns True).
- All elements equal: considered sorted.
- Array with negative numbers: handled correctly.
- Array with only one unsorted pair: detected efficiently.
---
# Other Approaches (if any)
- You could use Python's built-in `all()` and `zip()` for a more concise check:
  ```python
  def isSorted(arr):
      return all(x <= y for x, y in zip(arr, arr[1:]))
  ```
---
# Pythonic Tips and Tricks (if any)
- Use `all()` with a generator for elegant one-liners.
- Use `zip(arr, arr[1:])` to pair consecutive elements.
- Early exit in loops for efficiency.
---
# Programming Concepts Used
- **Iteration:** Looping through array elements.
- **Conditional Statements:** Checking order between elements.
- **Early Exit:** Breaking out of loop when unsorted order is found.
- **Boolean Logic:** Using flags to track sorted status.
---
