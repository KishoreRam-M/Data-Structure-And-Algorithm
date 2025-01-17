### Approach Name: **Prefix and Suffix Product Method** (also known as the **Two-Pass Product Method**)

### Description:
The **Prefix and Suffix Product Method** is a space-efficient technique to solve the "Product of Array Except Self" problem without using division. This method involves calculating the cumulative product of elements in two separate passes over the array:
1. **Prefix Product**: The product of all elements before the current index.
2. **Suffix Product**: The product of all elements after the current index.

### How to Use This Approach:

1. **Initialize**:
   - Create an output array initialized to 1. This will store the final result.
   - Use two temporary variables (`prefix` and `suffix`) to store the cumulative product for prefix and suffix respectively.

2. **Calculate Prefix Products**:
   - Iterate over the array from left to right.
   - For each index, store the cumulative product of all previous elements in the output array.
   - Update the `prefix` by multiplying it with the current element.

3. **Calculate Suffix Products**:
   - Iterate over the array from right to left.
   - For each index, multiply the existing value in the output array (which contains the prefix product) with the cumulative product of all elements after that index.
   - Update the `suffix` by multiplying it with the current element.

4. **Return the Output Array**:
   - After both passes, the output array will contain the product of all elements except the current one for each index.

### Step-by-Step Example:

#### Input:
```
arr = [10, 3, 5, 6, 2]
```

#### Steps:
1. **Prefix Pass**:
   - Start with `prefix = 1`.
   - Traverse from left to right:
     - For `i = 0`: `result[0] = prefix` → `result[0] = 1`, then `prefix *= arr[0]` → `prefix = 10`.
     - For `i = 1`: `result[1] = prefix` → `result[1] = 10`, then `prefix *= arr[1]` → `prefix = 30`.
     - For `i = 2`: `result[2] = prefix` → `result[2] = 30`, then `prefix *= arr[2]` → `prefix = 150`.
     - For `i = 3`: `result[3] = prefix` → `result[3] = 150`, then `prefix *= arr[3]` → `prefix = 900`.
     - For `i = 4`: `result[4] = prefix` → `result[4] = 900`, then `prefix *= arr[4]` → `prefix = 1800`.

   Intermediate `result` after prefix pass: `[1, 10, 30, 150, 900]`.

2. **Suffix Pass**:
   - Start with `suffix = 1`.
   - Traverse from right to left:
     - For `i = 4`: `result[4] *= suffix` → `result[4] = 900 * 1`, then `suffix *= arr[4]` → `suffix = 2`.
     - For `i = 3`: `result[3] *= suffix` → `result[3] = 150 * 2`, then `suffix *= arr[3]` → `suffix = 12`.
     - For `i = 2`: `result[2] *= suffix` → `result[2] = 30 * 12`, then `suffix *= arr[2]` → `suffix = 60`.
     - For `i = 1`: `result[1] *= suffix` → `result[1] = 10 * 60`, then `suffix *= arr[1]` → `suffix = 180`.
     - For `i = 0`: `result[0] *= suffix` → `result[0] = 1 * 180`, then `suffix *= arr[0]` → `suffix = 1800`.

   Final `result` after suffix pass: `[180, 600, 360, 300, 900]`.

#### Output:
```
[180, 600, 360, 300, 900]
```


### THE CODE ###
```
class Solution {
    public static int[] productExceptSelf(int arr[]) {
        int pos = 1; // Used to store the suffix product
        int pre = 1; // Used to store the prefix product
        int result[] = new int[arr.length]; // Result array to store the final products

        // Initialize result array with 1s
        for (int i = 0; i < arr.length; i++) {
            result[i] = 1;
        }

        // First loop: Calculate the prefix product for each element
        for (int i = 0; i < arr.length; i++) {
            result[i] *= pre; // Multiply the current result by the prefix product
            pre *= arr[i]; // Update the prefix product for the next iteration
        }

        // Second loop: Calculate the suffix product for each element
        for (int i = arr.length - 1; i >= 0; i--) {
            result[i] *= pos; // Multiply the current result by the suffix product
            pos *= arr[i]; // Update the suffix product for the next iteration
        }

        // Return the result array
        return result;
    }
}
```

### Advantages:
- **No Division**: This method avoids division, making it safe from division-related issues like division by zero.
- **Space Efficiency**: It uses only a constant amount of extra space (`O(1)` space complexity) since it modifies the output array in place.
- **Time Complexity**: The time complexity is `O(n)`, as it involves two linear passes over the array.

### When to Use:
- When you need to calculate the product of all elements except the current one in an array.
- When you want to avoid using division due to potential issues with zeroes in the array.
- When optimizing for space complexity while keeping time complexity efficient.

This approach is commonly used in competitive programming and interviews for its elegance and efficiency.
