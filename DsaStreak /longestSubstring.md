### The Code

      class Solution {
    public int longestSubarray(int[] arr, int k) {
        int maxLength = 0;
        int currentSum = 0;
        HashMap<Integer, Integer> sumIndexMap = new HashMap<>();
        
        for (int i = 0; i < arr.length; i++) {
            currentSum += arr[i];
            
            if (currentSum == k) {
                maxLength = i + 1;
            }
            
            int neededSum = currentSum - k;
            if (sumIndexMap.containsKey(neededSum)) {
                maxLength = Math.max(maxLength, i - sumIndexMap.get(neededSum));
            }
            
            // Store the first occurrence of the currentSum
            if (!sumIndexMap.containsKey(currentSum)) {
                sumIndexMap.put(currentSum, i);
            }
        }
        
        return maxLength;
    }
}






### Explanation of the Code:

The `longestSubarray` function finds the length of the longest subarray with a sum equal to `k`. 

#### Key Components:
1. **Variables**:
   - `maxLength`: Tracks the length of the longest subarray found with a sum equal to `k`.
   - `currentSum`: Maintains the cumulative sum of elements as we iterate through the array.
   - `sumIndexMap`: A `HashMap` that stores the first occurrence of each cumulative sum.

2. **Loop Through Array**:
   - Iterate through the array, updating `currentSum` at each step.
   - If `currentSum` equals `k`, the subarray from the start to the current index has the sum `k`. Update `maxLength` to `i + 1` (since indices are 0-based).

3. **Check for Needed Sum**:
   - Calculate `neededSum` as `currentSum - k`. This represents the cumulative sum that should have occurred before the current index to form a subarray with sum `k`.
   - If `neededSum` is in `sumIndexMap`, calculate the potential subarray length and update `maxLength` if it's greater than the current `maxLength`.

4. **Store Cumulative Sum**:
   - Store the current cumulative sum in `sumIndexMap` with its index if it's not already there. This ensures that only the earliest index is stored, maximizing the length of the subarray when the sum `k` is found again.

5. **Return Result**:
   - After iterating through the array, return `maxLength` as the length of the longest subarray with sum `k`.

### Visual Explanation:

#### Example:
- Given `arr = [1, -1, 5, -2, 3]` and `k = 3`.

1. **Initialization**:
   - `maxLength = 0`
   - `currentSum = 0`
   - `sumIndexMap = {}`

2. **Iteration through `arr`**:

   - **Index 0** (`arr[0] = 1`):
     - `currentSum = 1`
     - `neededSum = 1 - 3 = -2` (not in `sumIndexMap`)
     - Add `currentSum` to `sumIndexMap`: `{1: 0}`
     - No update to `maxLength`.

   - **Index 1** (`arr[1] = -1`):
     - `currentSum = 0`
     - `neededSum = 0 - 3 = -3` (not in `sumIndexMap`)
     - Add `currentSum` to `sumIndexMap`: `{1: 0, 0: 1}`
     - No update to `maxLength`.

   - **Index 2** (`arr[2] = 5`):
     - `currentSum = 5`
     - `neededSum = 5 - 3 = 2` (not in `sumIndexMap`)
     - Add `currentSum` to `sumIndexMap`: `{1: 0, 0: 1, 5: 2}`
     - No update to `maxLength`.

   - **Index 3** (`arr[3] = -2`):
     - `currentSum = 3`
     - `neededSum = 3 - 3 = 0` (found in `sumIndexMap` at index 1)
     - Calculate subarray length: `3 - 1 = 2`
     - Update `maxLength = 2`
     - Add `currentSum` to `sumIndexMap`: `{1: 0, 0: 1, 5: 2, 3: 3}`

   - **Index 4** (`arr[4] = 3`):
     - `currentSum = 6`
     - `neededSum = 6 - 3 = 3` (found in `sumIndexMap` at index 3)
     - Calculate subarray length: `4 - 3 = 1`
     - No update to `maxLength` since 1 < 2.
     - Add `currentSum` to `sumIndexMap`: `{1: 0, 0: 1, 5: 2, 3: 3, 6: 4}`

3. **Final Result**:
   - The longest subarray with sum `k = 3` is of length `2`.

### Summary:

- The function efficiently finds the longest subarray with a sum of `k` using a cumulative sum and a hashmap to track first occurrences of sums, allowing constant time lookups for potential subarray lengths. This approach avoids the need for a nested loop, making the solution more optimal with a time complexity of \(O(n)\).
