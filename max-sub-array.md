# PROBLEM : MAX SUB ARRAY
---
## Problem Link : [Max Sub Array - Leetcode](https://leetcode.com/problems/maximum-subarray/)

## Difficulty Level : ![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)
---
# STATEMENT
You will be provided with an **array**.
You need to **find the maximum subarray sum**.

* A **subarray** is a **contiguous sequence of elements** in the array.
* If the elements are **not contiguous**, then it is called a **subsequence**.

**Example:**
```python
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
# Maximum subarray sum = 7, from subarray [4, -1, -2, 1, 5]
```

**Summary:**
* Subarray → contiguous elements.
* Subsequence → elements in order, but can skip some.
* Maximum subarray sum → largest sum among all subarrays.

---
# BRUTE FORCE : 1
## Intuition – Maximum Subarray Sum (3-loop brute-force approach)
1. You want to find the **maximum sum of any contiguous subarray**.
2. Initialize `max_sum` to the lowest possible value (e.g., `-infinity`).
3. Use **three nested loops**:
   - **Outer loop (`i`)**: Choose the starting index of the subarray.
   - **Middle loop (`j`)**: Choose the ending index of the subarray (inclusive).
   - **Inner loop (`k`)**: Sum all elements from `i` to `j` to get `sub_sum`.
4. After calculating `sub_sum` for each subarray:
   - Compare it with `max_sum`.
   - If `sub_sum > max_sum`, update `max_sum`.
5. Repeat for all possible subarrays to ensure **all contiguous subarrays are considered**.
6. Finally, `max_sum` contains the **maximum subarray sum**.

✅ **Key Idea:**
- This is a **brute-force approach**, checking all possible subarrays.
- Using a running sum inside the inner loop avoids recalculating sums from scratch for each subarray, but the time complexity is still **O(n³)** due to three nested loops.

## Code
```python
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
max_sum = float("-inf")
for i in range(len(arr)):
  for j in range(i+1, len(arr)+1):
    sub_sum = 0
    for k in range(i,j):
      sub_sum += arr[k]
    if sub_sum > max_sum : max_sum = sub_sum
    print(arr[i:j], f"sub-array-sum : {sub_sum}")
print(max_sum)
```

---
## Time and Space Complexity
### **Time Complexity** ![O(n³)](https://img.shields.io/badge/Time%20Complexity-O(n%C2%B3)-red)
1. Three nested loops: start, end, and sum calculation.
2. O(n × n × n) = O(n³) operations for all subarrays.
3. Slicing/printing each subarray also takes O(n) per operation, but the main bottleneck is the three loops.
✅ So:
- **Total time complexity:** O(n³)

### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only `sub_sum` and `max_sum` are stored → O(1).
2. Temporary slices (like `arr[i:j+1]`) use extra space, but only while printing.
   - Maximum slice size = n → O(n) temporarily.
✅ So:
- Auxiliary space: O(1)
- Including temporary slices: O(n)

### **Summary**
- **Time Complexity:** Three nested loops → O(n³)
- **Space Complexity:** Few variables → O(1), temporary slices → O(n)

---
# BRUTE FORCE 2
## Intuition
1. You want to find the **maximum sum of any contiguous subarray**.
2. Start from each index `i` in the array.
3. For each `i`, consider all subarrays that start at `i`:  `[i]`, `[i:i+1]`, `[i:i+2]`, …
4. Keep a running sum `sub_sum` for the current subarray.
5. After adding each element, check if `sub_sum` is larger than `max_sum`, and update `max_sum` if needed.
6. Repeat for all starting indices to ensure **all subarrays are considered**.

✅ This approach **brute-forces all subarrays** but avoids recalculating sums from scratch by using a running sum.

## Code
```python
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
n = len(arr)
max_sum = float("-inf")
for i in range(n):
    sub_sum = 0
    for j in range(i, n):
        sub_sum += arr[j]
        print(arr[i:j+1], f"sub-array-sum: {sub_sum}")
        if sub_sum > max_sum:
            max_sum = sub_sum
print("Maximum subarray sum:", max_sum)
```

---
## Time and Space Complexity
### **Time Complexity** ![O(n²)](https://img.shields.io/badge/Time%20Complexity-O(n%C2%B2)-blue)
1. Two nested loops: start and end indices.
2. O(n × n) = O(n²) operations for all subarrays.
3. Slicing/printing each subarray also takes O(n) per operation, so total printing cost is O(n³).
✅ So:
- **Without slicing:** O(n²)
- **With slicing for printing:** O(n³)

### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only variables `sub_sum` and `max_sum` are stored → **constant space** → O(1).
2. Temporary slices for printing (`arr[i:j+1]`) use extra space, but only temporarily.
   - Maximum slice size = n → O(n) temporarily.
✅ So:
- Auxiliary space: O(1)
- Including temporary slices: O(n)

### **Summary**
- **Time Complexity:** Two nested loops → O(n²), with slicing/printing → O(n³)
- **Space Complexity:** Few variables → O(1), temporary slices → O(n)

---
# OPTIMIZED
## ALGO : KADANE'S
### 1. Initialize
- `curr_sum = 0`
- `max_sum = lowest possible value`

### 2. Iterate through the array elements
- For each element `n`, **add it to `curr_sum`**.

### 3. Update maximum
- If `curr_sum > max_sum`, update `max_sum = curr_sum`.

### 4. Reset if negative
- If `curr_sum` becomes negative, **reset it to 0**.
- **Reason:** Carrying a negative sum would reduce future subarray sums.
- Effectively, we **discard the previous subarray** and **start fresh from the next element**.

### 5. Element choice
Each element has a choice:
1. **Contribute to the current sum** (if it keeps `curr_sum` positive).
2. **Not contribute** and let the next element start a new subarray in hopes of finding a larger sum later.

## Code
```python
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
curr_sum = 0
max_sum = float("-inf")
start = 0
end = 0
temp_start = 0
for i in range(len(arr)):
      curr_sum += arr[i]
      if curr_sum > max_sum:
            max_sum = curr_sum
            start = temp_start
            end = i
      if curr_sum < 0:
            curr_sum = 0
            temp_start = i + 1
print(max_sum)
print(arr[start:end+1])
```
---
## Time and Space Complexity
### **Time Complexity** ![O(n)](https://img.shields.io/badge/Time%20Complexity-O(n)-blue)
1. The algorithm **iterates through the array only once** → n iterations.
2. For each element:
   - Add it to `curr_sum` → O(1)
   - Compare and update `max_sum` → O(1)
   - Reset `curr_sum` if negative → O(1)
✅ Total time complexity: **O(n)**

### **Space Complexity** ![O(1)](https://img.shields.io/badge/Space%20Complexity-O(1)-green)
1. Only a few variables are used:
   - `curr_sum`, `max_sum`, `start`, `end`, `i` → O(1)
✅ Auxiliary space: **O(1)**
- No additional arrays or slices are created.

### **Summary**
- **Time Complexity:** O(n) → single pass through the array
- **Space Complexity:** O(1) → only a few variables used

---
### Edge Cases
- If the array is empty, the result should be handled (e.g., return 0 or None).
- If all elements are negative, the maximum subarray is the largest single element.
### Pythonic Tips
- Use `float('-inf')` for initializing the minimum possible value.
- List comprehensions and built-in functions like `max()` can sometimes simplify code, but for this problem, a loop is most efficient.
- Use `enumerate()` for cleaner index tracking if needed.
### Programming Concepts Used
- **Dynamic Programming:** Kadane's Algorithm uses optimal substructure and overlapping subproblems.
- **Greedy Approach:** Always keep the best sum so far and reset when the sum is negative.
- **Nested Loops (Brute-force):** Used to check all possible subarrays.

---

**Note:**
This is the most **efficient way** to find the maximum subarray sum, compared to the 2-loop or 3-loop methods.
