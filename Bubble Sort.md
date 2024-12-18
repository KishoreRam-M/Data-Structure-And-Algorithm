# Bubble Sort

Bubble Sort is a basic sorting algorithm commonly used to understand the fundamental concept of sorting. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order.

---

## Algorithm

1. Iterate through the array multiple times.
2. During each pass, compare adjacent elements.
3. Swap them if the left element is greater than the right.
4. Repeat until the array is sorted.

---

## Java Code

java
    
     for (int i = 0; i < arr.length - 1; i++) {
    for (int j = 0; j < arr.length - 1 - i; j++) { // Adjusted range for j
        if (arr[j] > arr[j + 1]) {
            // Swap arr[j] and arr[j+1]
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
     }
     ## Time Complexity

| Case       | Complexity | Explanation                                                                 |
|------------|------------|-----------------------------------------------------------------------------|
| **Best**   | **O(n)**   | When the array is already sorted (can include an optimization to detect this). |
| **Average**| **O(n²)**  | Occurs in the average case with random elements.                            |
| **Worst**  | **O(n²)**  | Happens when the array is sorted in reverse order.                          |

### Details
In the worst case, the algorithm performs approximately \( \frac{n(n-1)}{2} \) comparisons.

---

## Space Complexity

| Type          | Complexity | Explanation                                             |
|---------------|------------|---------------------------------------------------------|
| **Auxiliary** | **O(1)**   | Bubble Sort is an **in-place algorithm** (no extra space needed). |
