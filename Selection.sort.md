# Selection Sort

**Selection Sort** is an intuitive sorting algorithm that sorts an array by repeatedly selecting the smallest (or largest) element from the unsorted portion and moving it to the sorted portion.

---

## How It Works

1. Divide the array into two parts:
   - The **sorted portion** (initially empty).
   - The **unsorted portion** (initially the entire array).
2. Find the smallest element in the unsorted portion.
3. Swap the smallest element with the first element of the unsorted portion.
4. Move the boundary between the sorted and unsorted portions by one.
5. Repeat until the entire array is sorted.

---

## Java Code

```java
class Solution {
    void selectionSort(int[] arr) {
        // Loop over each element in the array
        for (int i = 0; i < arr.length; i++) {
            int min = i; // Assume the current index is the minimum
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[min] > arr[j]) { // Find the index of the smallest element
                    min = j;
                }
            }
            // Swap the current element with the smallest element
            int temp = arr[i];
            arr[i] = arr[min];
            arr[min] = temp;
        }
    }
}
```

---

## Example Walkthrough

### Input Array:  
**[64, 25, 12, 22, 11]**

### Step-by-Step Sorting:
1. Find the smallest element in the entire array (11) and swap it with the first element.  
   **Result**: [11, 25, 12, 22, 64]  

2. Find the smallest element in the unsorted portion (12) and swap it with the second element.  
   **Result**: [11, 12, 25, 22, 64]  

3. Find the smallest element in the remaining unsorted portion (22) and swap it with the third element.  
   **Result**: [11, 12, 22, 25, 64]  

4. Continue until the entire array is sorted.  
   **Final Output**: [11, 12, 22, 25, 64]  

---

## Time and Space Complexity

| **Aspect**       | **Complexity** | **Explanation**                                                                |
|-------------------|----------------|--------------------------------------------------------------------------------|
| **Best Case**     | **O(n²)**      | Always performs \( n(n-1)/2 \) comparisons regardless of the input.            |
| **Average Case**  | **O(n²)**      | Occurs in random cases; depends on the size of the input array.                |
| **Worst Case**    | **O(n²)**      | Performs the maximum number of comparisons and swaps when array is reversed.   |
| **Space Usage**   | **O(1)**       | In-place algorithm; uses no additional memory beyond a few temporary variables.|

---

## Key Points

- **Advantages**:
  - Simple and easy to implement.
  - Requires minimal additional memory.
- **Disadvantages**:
  - Inefficient for large datasets.
  - Performs unnecessary comparisons even when the array is already sorted.
- **Use Case**:
  - Suitable for small datasets or when memory constraints are critical.
