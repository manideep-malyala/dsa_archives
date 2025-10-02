
# Problem : Add to Array-Form of Integer
---
## Problem Link : [Add to Array-Form of Integer - LeetCode](https://leetcode.com/problems/add-to-array-form-of-integer/)
---
## Difficulty Level : 
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)

---
# Statement 

**Detailed Problem Statement:**

We are given a non-negative integer num represented as an array of digits `num`, where each `num[i]` is a digit of the number (with the most significant digit at `num[0]`). We are also given an integer `k`.

We need to return the array-form of the sum of the integer represented by the array and the integer `k`. The array-form of an integer contains all its digits in left-to-right order (most significant to least significant).

**Example 1:**

```
Input: num = [1,2,0,0], k = 34
Output: [1,2,3,4]
Explanation: 1200 + 34 = 1234
```

**Example 2:**

```
Input: num = [2,7,4], k = 181
Output: [4,5,5]
Explanation: 274 + 181 = 455
```

**Example 3:**

```
Input: num = [2,1,5], k = 806
Output: [1,0,2,1]
Explanation: 215 + 806 = 1021
```

**Constraints:**
- `1 <= num.length <= 10^4`
- `0 <= num[i] <= 9`
- `0 <= k <= 10^4`

**Summary:**
* You are given a number in digit-array form and another as an integer.
* Add both numbers.
* Return the result as an array of digits, preserving order.

---
# Optimized Approach
---
### Intuition

1. The array `num` represents a big integer (possibly up to 10,000 digits), which may not fit in a standard integer type.
2. We want to add the integer `k` to `num` and return the result in the same array-form.
3. Since addition starts from the least significant digit (rightmost), we traverse `num` from the end. For each digit, we add the corresponding digit of `k` (rightmost digit of k), handle carry-over, and move to the next digit to the left.
4. If `k` still has digits (or there is still carry left) after finishing the array, we keep inserting those digits at the start of the array.

✅ **Key Idea:**
- Treat the addition like how you do it by hand: rightmost digit to leftmost, carrying over any overflowing value.
---
### Pseudocode

```
carry = k
for i from len(num)-1 down to 0:
    total = num[i] + carry
    carry = total // 10
    num[i] = total % 10

while carry > 0:
    insert carry % 10 at start of num
    carry = carry // 10

return num
```

---
### Code
```python
from typing import List

def addToArrayForm(self, num: List[int], k: int) -> List[int]:
    carry = k 
    p = len(num)-1
    for i in range(p, -1, -1):
        carry, num[i] = divmod(num[i]+carry, 10)
    while carry:
        num.insert(0, carry % 10)
        carry //= 10 
    return num
```
---

### Explanation

Let's break down the optimized approach step by step (Chain of Thought):

1. **Initialization:**
   - `carry = k`: We use `carry` to represent both the value of `k` and any additional carry from previous addition steps.
   - `p = len(num)-1`: Start from the rightmost (least significant) digit of `num`.

2. **Main Loop (from last digit to first):**
   - For each digit from the end towards the beginning:
       - Add the current digit of `num` and the current `carry`.
       - Use `divmod` to separate the new digit (`num[i]`) and the new `carry`. 
         - `divmod(a, b)` returns `(a // b, a % b)`.
         - For example, if `num[i]=2`, `carry=9`, then `divmod(2+9, 10)` yields `(1,1)`, so `carry=1`, `num[i]=1`.
   - This allows us to both update the digit and pass the new carry to the next higher digit.

3. **Handle Remaining carry/k:**
   - After the loop, if there's still any `carry` left (meaning the sum is longer than the input array), we keep adding its digits to the front (`num.insert(0, carry % 10)`), and reduce `carry`.
   - This step ensures that the answer can grow longer than the original input.

4. **Return the result:**
   - The final array `num` has the correct digits in array-form.

#### Example Walkthrough
Let's take `num = [2, 7, 4]`, `k = 181`.

- Initial: num = [2,7,4], carry = 181
    - i=2: add 4 + 181 = 185, carry, num[2] = divmod(185,10) = (18,5) => num=[2,7,5], carry=18
    - i=1: add 7 + 18 = 25, carry, num[1] = divmod(25,10) = (2,5) => num=[2,5,5], carry=2
    - i=0: add 2 + 2 = 4, carry, num[0] = divmod(4,10) = (0,4) => num=[4,5,5], carry=0
- carry=0, so while loop is skipped.
- Return: [4,5,5]

---

### Time and Space Complexity
#### **Time Complexity** ![Time Complexity](https://img.shields.io/badge/Time-O(N%20%2B%20logK)-yellow)
1. The for-loop runs O(N) times, where N is the length of `num`.
2. The while-loop runs O(logK) times, only when there is leftover `carry` (which is up to the number of digits in k, at most logK).
3. So, total time is O(N + logK).

#### **Space Complexity** ![Space Complexity](https://img.shields.io/badge/Space-O(1)-green) (not counting the result)
1. We modify the input array in-place, so apart from a few variables, no extra space is used.
2. In the worst case, we insert at most O(log(sum)) digits at the start. But since the output must store all digits anyway, auxiliary space is O(1).

### **Summary**
- **Time Complexity:** O(N + logK), where N = len(num)
- **Space Complexity:** O(1) (excluding the result array)
---

# Edge Cases

- **num is much longer than k**: The addition continues with just the digits of `num`.
- **k is much longer than num**: The code handles the additional digits via the while loop.
- **Carry-over is needed at the most significant digit**: E.g., [9,9,9] + 2 = [1,0,0,1].
- **k or num is zero**: Code still works, as the carry just comes from the nonzero number.
- **num is a single-digit array**: Generalizes with no special handling required.

---
# Other Approaches (if any)

- **Simple Naive Approach:** Convert the whole number array to an integer, add to k, and split back to a digit array. However, for very large arrays, this is not feasible due to integer overflow or performance cost.
- **Reverse List and Use While Loop:** Reverse num, add k digit-by-digit from the start, then reverse the result, similar in logic to optimized.

---

# Pythonic Tips and Tricks (if any)

- **Using divmod:** `carry, num[i] = divmod(num[i] + carry, 10)` is a concise way to perform both quotient and remainder in a single statement.
- **List insert:** `num.insert(0, value)` is used to efficiently insert digits at the front. Be aware that for large lists, this has O(N) time per operation, but for the number of insertions (usually small, ~logK), this is negligible compared to overall algorithm time.
- **Variable reuse:** Using `carry` for both temporary addition and as a working variable is concise.
- **No need to manually split k into digits:** By using modulo and integer division in the carry handling, we avoid explicit conversion.

---

# Programming Concepts Used

- **Simulating Manual Addition:** Just like how you add two numbers on paper, digit by digit from right to left with carry.
- **List Manipulation:** Updating values in a list, inserting at the beginning.
- **Looping from Right to Left:** By looping backwards, we process least significant digits first.
- **Integer Division and Modulo Operations:** To extract digits and manage carry-over.
- **In-place Array Modification:** Instead of constructing new arrays, the existing list is updated as much as possible.

---
```
