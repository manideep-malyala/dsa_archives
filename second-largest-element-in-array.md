# Problem : Second Largest Element in the Array
---
## Problem Link : [Second Largest Element - GeeksforGeeks](https://www.geeksforgeeks.org/problems/second-largest3735/1)
---
## Difficulty Level :

![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

---
# Statement 

Given an array of integers, find the second largest element in the array. The second largest element is the largest element that is strictly less than the maximum element. If all elements are the same, or the array has less than two distinct elements, the second largest does not exist.

**Example:**

```python
arr = [1, 3, 2, 4, 9, 13, 2, 91, 21, 82]
# Largest element: 91
# Second largest element: 82
```

**Summary:**
* Find the largest and second largest elements in the array.
* The second largest must be strictly less than the largest.
* Handle cases with duplicate maximums and arrays with less than two distinct elements.

---
# Brute-Force Approach

### Intuition
1. Sort the array in ascending order.
2. The largest element is at the end of the sorted array.
3. Traverse the sorted array from the end to find the first element that is not equal to the largest (this is the second largest).
4. If all elements are the same, return -1 (or indicate no second largest exists).

✅ **Key Idea:**
- Sorting brings the largest elements to the end, making it easy to find the second largest by scanning backwards.

---
### Pseudocode
1. Sort the array.
2. Set `second_largest` to -1.
3. Traverse from the end of the array:
   - If current element is not equal to the last element (largest), set `second_largest` and break.
4. Return `second_largest`.

---
### Code
```python
arr =  [ 1, 3, 2, 4, 9, 13, 2, 91, 21, 82]

second_largest_ = -1
arr.sort()
for i in range(len(arr)-1, -1, -1):
  if arr[i] != arr[-1]:
    second_largest_ = arr[i]
    break
print(second_largest_)

# O(N log N) + O(N) bruteforce
```
---
### Explanation
- The array is sorted so the largest element is at the last index.
- Loop backwards from the end:
  - If an element is found that is not equal to the largest, it is the second largest.
  - If no such element is found, all elements are the same, so return -1.
- Sorting takes O(N log N) time, and the loop is O(N).

---
### Time and Space Complexity
#### **Time Complexity** ![O(N log N)](https://img.shields.io/badge/Time%20Complexity-O(N%20log%20N)-red)
1. Sorting the array: O(N log N)
2. Scanning for second largest: O(N)

#### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only a few variables are used for tracking.
2. Sorting may use extra space depending on implementation, but typically O(1) for in-place sort.

### **Summary**
- **Time Complexity:** O(N log N)
- **Space Complexity:** O(1)

---
# Brute-Force Approach 2

### Intuition
1. Find the largest element in the array with one pass.
2. In a second pass, find the largest element that is not equal to the largest (i.e., the second largest).
3. If all elements are the same, the second largest does not exist.

✅ **Key Idea:**
- Two separate passes: first for the largest, second for the second largest.

---
### Pseudocode
1. Initialize `largest` to the first element.
2. Loop through the array to find the largest.
3. Initialize `second_largest` to negative infinity.
4. Loop through the array:
   - If element is greater than `second_largest` and not equal to `largest`, update `second_largest`.
5. Return `second_largest`.

---
### Code
```python
arr =  [ 1, 3, 2, 4, 9, 13, 2, 91, 21, 82]

# first pass
largest_ = arr[0]
for i in range(1, len(arr)):
  if arr[i] > largest_ : largest_ = arr[i]

# second pass
second_largest_ = float("-inf")
for i in range(len(arr)):
  if arr[i] > second_largest_ and arr[i] != largest_ :
    second_largest_ = arr[i]

print(largest_, second_largest_)

# O(2N)
```
---
### Explanation
- First loop finds the largest element.
- Second loop finds the largest element that is not equal to the largest (second largest).
- Handles duplicate maximums and negative numbers.
- Both loops are O(N), so total time is O(2N) = O(N).

---
### Time and Space Complexity
#### **Time Complexity** ![O(N)](https://img.shields.io/badge/Time%20Complexity-O(N)-blue)
1. First pass: O(N)
2. Second pass: O(N)

#### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only a few variables are used.

### **Summary**
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

---
# Optimized Approach
---

### Intuition
1. Find both the largest and second largest in a single pass.
2. Track the largest and second largest as you iterate.
3. If a new largest is found, update second largest to previous largest.
4. If current element is less than largest but greater than second largest, update second largest.

✅ **Key Idea:**
- Efficiently find both values in one traversal, minimizing time.

---
### Pseudocode
1. Initialize `largest` to first element, `second_largest` to negative infinity.
2. Loop through the array starting from the second element:
   - If current > largest:
     - Update `second_largest` to `largest`.
     - Update `largest` to current.
   - Else if current < largest and current > second_largest:
     - Update `second_largest` to current.
3. Return `second_largest`.

---
### Code
```python
arr =  [ 1, 3, 2, 4, 9, 13, 2, 91, 21, 82]

largest_ = arr[0]
s_largest_ = float("-inf")
for i in range(1, len(arr)):
  if arr[i] > largest_ :
    s_largest_ = largest_
    largest_ = arr[i]
  elif arr[i] < largest_ and arr[i] > s_largest_ :
    s_largest_ = arr[i]
print(s_largest_)
```
---
### Explanation
- Start with the first element as the largest.
- For each element:
  - If it is greater than the current largest, update second largest to previous largest, and largest to current.
  - If it is less than largest but greater than second largest, update second largest.
- Only one pass through the array is needed.

---
### Time and Space Complexity
#### **Time Complexity** ![O(N)](https://img.shields.io/badge/Time%20Complexity-O(N)-blue)
1. Single pass through the array: O(N)

#### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only a few variables are used.

### **Summary**
- **Time Complexity:** O(N)
- **Space Complexity:** O(1)
---

# Edge Cases
- Array with all elements the same: No second largest exists.
- Array with only one element: No second largest exists.
- Array with negative numbers: Works as expected.
- Array with two distinct elements: Second largest is the smaller one.

---
# Other Approaches (if any)
- Using built-in Python functions like `set()` and `max()` to find unique elements and the second largest, but may be less efficient for large arrays.

---
# Pythonic Tips and Tricks (if any)
- Use `float('-inf')` for initializing the minimum possible value.
- Use built-in functions like `max()` and `set()` for quick solutions in interviews.
- List comprehensions can help filter unique elements.

---
# Programming Concepts Used
- **Sorting:** Used in brute-force approach to simplify finding largest elements.
- **Two-pass scanning:** Used to find largest and second largest separately.
- **Single-pass scanning:** Used in the optimal approach for efficiency.
- **Edge case handling:** Ensures robustness for all input types.

---
