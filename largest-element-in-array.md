# PROBLEM : LARGEST ELEMENT IN THE ARRAY
---
## Problem Link : [Largest Element in Array](https://www.geeksforgeeks.org/problems/largest-element-in-array4009/1)
---
## Difficulty Level
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

---
## Brute-Force Approach

---
### Pseudocode
1. Given an array of numbers.
2. Sort the array in ascending order.
3. The largest element will be the last element after sorting.
4. Print the last element of the sorted array.

---
### Code
```python
# BRUTE FORCE APPROACH
arr =  [ 1, 3, 2, 4, 9, 13, 2, 91, 21, 82]

# Sort the array
arr.sort()
# Print the last element (largest)
print(arr[-1])
```
---
### Explanation
- Start with the given array.
- Use the built-in `sort()` method to arrange elements in ascending order.
- The largest element will always be at the last index after sorting.
- Print the last element using `arr[-1]`.
- This approach is simple but not the most efficient, as sorting takes extra time.

---
### Time and Space Complexity
![Time Complexity](https://img.shields.io/badge/Time%20Complexity-O(n%20log%20n)-orange)
![Space Complexity](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
- Sorting the array takes O(n log n) time due to comparison-based sorting algorithms.
- Only a constant amount of extra space is used (in-place sort).

---
## Optimized Approach
---
### Pseudocode
1. Given an array of numbers.
2. Initialize a variable `largest_` to the first element.
3. Loop through the array starting from the second element.
4. For each element, compare it with `largest_`.
5. If the current element is greater, update `largest_`.
6. After the loop, print `largest_`.

---
### Code
```python
# OPTIMAL APPROACH
arr =  [ 1, 3, 2, 4, 9, 13, 2, 91, 21, 82]

largest_ = arr[0]
for i in range(1, len(arr)):
  if arr[i] > largest_ : largest_ = arr[i]
print(largest_)
```
---
### Explanation
- Start with the first element as the largest.
- Iterate through the rest of the array.
- For each element, check if it is greater than the current largest.
- If so, update the largest value.
- After checking all elements, the variable holds the largest value.
- This approach only requires a single pass through the array.

---
### Time and Space Complexity
![Time Complexity](https://img.shields.io/badge/Time%20Complexity-O(n)-blue)
![Space Complexity](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
- Only one loop through the array, so O(n) time.
- Only a few variables are used, so O(1) space.

---
## Other Approaches (if any)
- You can use Python's built-in `max()` function: `max(arr)` for a concise solution.

---
## Pythonic Tips and Tricks (if any)
- Use `max(arr)` for the most concise and readable way to find the largest element.
- List comprehensions and generator expressions can be used for more complex conditions.
- Use `arr[-1]` to access the last element of a list.

---
## Programming Concepts Used
- **Iteration:** Looping through elements to compare values.
- **Comparison Operators:** Using `>` to find the largest value.
- **In-place Sorting:** Modifying the array directly with `sort()`.
- **Indexing:** Accessing elements by their position in the array.

---
