###  The Code:Larget Subarray 0 and 1  ###
     class Solution {
    public int maxLen(int[] arr) {
        int sum = 0;
        int subarray = 0;
        
        // Map to store the first occurrence of sum
        Map<Integer, Integer> map = new HashMap<>();
        
        // Iterate through the array
        for (int i = 0; i < arr.length; i++) {
            // Convert 0 to -1 for easier sum calculation
            if (arr[i] == 0) {
                arr[i] = -1;
            }
            
            // Add current element to sum
            sum += arr[i];

            // If sum is 0, update subarray length
            if (sum == 0) {
                subarray = i + 1;
            }

            // If sum has been seen before, calculate the length of the subarray
            if (map.containsKey(sum)) {
                subarray = Math.max(subarray, i - map.get(sum));
            } else {
                // Store the sum and its index
                map.put(sum, i);
            }
        }

        // Corrected return statement, outside the loop
        return subarray;  // Returns the length of the longest subarray with sum 0
    }
}



### **Code Explanation:**

This code is designed to find the **length of the longest subarray with a sum of 0** in an array. The basic idea is to traverse through the array, compute the cumulative sum (starting from index 0), and use a HashMap to keep track of the sums we've encountered so far. If the cumulative sum repeats at some later index, it means there is a subarray between the two indices whose sum is 0.

### **Detailed Step-by-Step Explanation:**

#### 1. **Initialization:**
   - **sum**: This variable keeps track of the cumulative sum of elements in the array as we iterate through it.
   - **subarray**: This variable stores the length of the longest subarray with a sum of 0.
   - **map**: A HashMap is used to store the cumulative sum and its corresponding index. This allows us to check if a cumulative sum has appeared before efficiently.

#### 2. **Looping Through the Array:**
   We loop through each element of the array and perform the following operations:
   
   - If the element is `0`, we treat it as `-1`. This simplifies the problem because instead of finding a sum of `0`, we're now looking for a sum of `0` or balancing out the array to find subarrays with zero sum.
   
   - We calculate the **cumulative sum** (`sum`) as we iterate.
   
   - If the `sum` is `0`, it means that the subarray from index `0` to the current index has a sum of 0. We update `subarray` to the length of this subarray, i.e., `i + 1`.
   
   - If the cumulative sum has been encountered before, it means there's a subarray between the previous index where the sum occurred and the current index with a sum of `0`. We calculate the length of this subarray and update `subarray` accordingly.
   
   - If the cumulative sum hasn't been encountered before, we store the current sum and its index in the HashMap.

#### 3. **Return the Result:**
   After the loop completes, the variable `subarray` will contain the length of the longest subarray whose sum is `0`.

### **Code Walkthrough with Example:**

Consider the array: `arr = {1, -1, 3, 2, -2, -3, 3, 1, -1, -1}`

#### Initial values:
- `sum = 0`
- `subarray = 0`
- `map = {}` (empty HashMap)

We now process each element of the array.

---

1. **i = 0 (arr[0] = 1):**
   - `sum = 0 + 1 = 1`
   - `sum != 0`, so no update to `subarray`
   - `map = {1: 0}` (storing sum and index)

---

2. **i = 1 (arr[1] = -1):**
   - `sum = 1 + (-1) = 0`
   - `sum == 0`, so `subarray = i + 1 = 1 + 1 = 2`
   - `map = {1: 0}` (no change)

---

3. **i = 2 (arr[2] = 3):**
   - `sum = 0 + 3 = 3`
   - `sum != 0`, so no update to `subarray`
   - `map = {1: 0, 3: 2}` (storing sum and index)

---

4. **i = 3 (arr[3] = 2):**
   - `sum = 3 + 2 = 5`
   - `sum != 0`, so no update to `subarray`
   - `map = {1: 0, 3: 2, 5: 3}` (storing sum and index)

---

5. **i = 4 (arr[4] = -2):**
   - `sum = 5 + (-2) = 3`
   - `sum already exists in map at index 2`
   - `subarray = Math.max(subarray, i - map.get(sum)) = Math.max(2, 4 - 2) = 2`

---

6. **i = 5 (arr[5] = -3):**
   - `sum = 3 + (-3) = 0`
   - `sum == 0`, so `subarray = i + 1 = 5 + 1 = 6`
   - `map = {1: 0, 3: 2, 5: 3, 0: 5}`

---

7. **i = 6 (arr[6] = 3):**
   - `sum = 0 + 3 = 3`
   - `sum already exists in map at index 2`
   - `subarray = Math.max(subarray, i - map.get(sum)) = Math.max(6, 6 - 2) = 6`

---

8. **i = 7 (arr[7] = 1):**
   - `sum = 3 + 1 = 4`
   - `sum != 0`, so no update to `subarray`
   - `map = {1: 0, 3: 2, 5: 3, 0: 5, 4: 7}`

---

9. **i = 8 (arr[8] = -1):**
   - `sum = 4 + (-1) = 3`
   - `sum already exists in map at index 2`
   - `subarray = Math.max(subarray, i - map.get(sum)) = Math.max(6, 8 - 2) = 6`

---

10. **i = 9 (arr[9] = -1):**
    - `sum = 3 + (-1) = 2`
    - `sum != 0`, so no update to `subarray`
    - `map = {1: 0, 3: 2, 5: 3, 0: 5, 4: 7, 2: 9}`

### **Final Result:**
- `subarray = 6`
- The longest subarray with a sum of 0 is from index `0` to `5`, with length `6`.

### **Visual Explanation (Diagram):**

Let’s visualize how the array is processed:

```
Array: [ 1, -1, 3, 2, -2, -3, 3, 1, -1, -1 ]
Index:   0   1   2   3   4   5   6   7   8   9
Cumulative Sum:
         1   0   3   5   3   0   3   4   3   2
Subarray Length:
   0   2       2       2   6   6   6   6
```



  ### **Prefix Sum with HashMap Approach - Use Cases and Examples**

The **Prefix Sum with HashMap** approach is commonly used to efficiently solve problems where you need to find subarrays that satisfy certain conditions (like a sum equal to 0 or a specific value). Below are a few common use cases with explanations.

---

### **1. Longest Subarray with Sum 0**

**Problem:**
Given an array, find the length of the longest subarray whose sum is 0.

**Use Case:**
When you need to find the longest subarray that balances out to a sum of 0, the **Prefix Sum with HashMap** approach is ideal. By iterating through the array and calculating cumulative sums, we can easily track when a subarray sum returns to 0 or repeats. This tells us that there is a subarray that balances to 0 between those indices.

#### **Example:**
Array: `[1, -1, 3, 2, -2, -3, 3, 1, -1, -1]`

- As you calculate the cumulative sum, you notice that when the sum equals `0` at various points, it indicates a subarray that sums to 0.
- You also notice that the same cumulative sum occurs at different points in the array, which means that the elements between those points sum to 0.

**Output:**
The longest subarray with sum 0 has a length of 6 (from index 0 to 5).

---

### **2. Subarray with Sum Equal to K**

**Problem:**
Find the longest subarray with a given sum `k`.

**Use Case:**
If you are given a specific sum `k` and need to find the longest subarray that sums to `k`, you can use the **Prefix Sum with HashMap** approach. By checking if the difference between the current cumulative sum and `k` has been seen before, you can identify subarrays that sum to `k`.

#### **Example:**
Array: `[1, 2, 3, -2, -1, 4]`, k = `3`

- As you calculate the cumulative sum and track its occurrences in the map, you can quickly find that a subarray from index 0 to 2 sums to `3`.

**Output:**
The longest subarray with sum 3 is from index 0 to 2 (length 3).

---

### **3. Subarray with Sum Equal to 0 in a Circular Array**

**Problem:**
Find a subarray with sum 0 in a circular array (array where the last element connects to the first element).

**Use Case:**
For circular array problems, where the subarrays might "wrap around" the end of the array, the **Prefix Sum with HashMap** approach can be extended. You can first apply the regular approach on the array and then consider subarrays that wrap around by combining the beginning and end of the array.

#### **Example:**
Array: `[8, -8, 1, 3, 4]`, k = `3`

- Here, you apply the **Prefix Sum with HashMap** method to find subarrays and then check for wraparound subarrays by treating the array as circular.

---

### **4. Count Subarrays with Sum 0**

**Problem:**
Count the number of subarrays whose sum is 0.

**Use Case:**
Instead of finding just one subarray, you might need to count how many subarrays have a sum of 0. By calculating the cumulative sum and checking if it repeats, you can count all such subarrays efficiently.

#### **Example:**
Array: `[1, -1, 1, -1]`

- By tracking the cumulative sum and checking if it repeats, you can determine how many subarrays have a sum of 0.

**Output:**
There are 4 subarrays with sum 0.

---

### **5. Subarray with Sum Equal to K After Removing K Elements**

**Problem:**
Find the longest subarray with sum equal to `k` after removing up to `k` elements.

**Use Case:**
In advanced problems where you can remove a fixed number of elements to get the sum `k`, the **Prefix Sum with HashMap** approach can be adapted. By tracking the cumulative sum and adjusting it based on the number of removals allowed, this approach helps solve such problems efficiently.

---

**LINK**
 (https://youtu.be/9ZyLjjk536U?si=i__A49QvBaIcCYXu)
