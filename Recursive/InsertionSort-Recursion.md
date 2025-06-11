# 🔄 Recursive Insertion Sort – Ultimate Guide

---

## ✳️ What is Insertion Sort?

**Insertion Sort** builds the sorted array **one element at a time** by comparing each new element with the sorted portion and inserting it at the correct position.

---

## ❓ Why Use Recursion in Insertion Sort?

| Reason          | Explanation                                             |
| --------------- | ------------------------------------------------------- |
| Learn Recursion | Helps visualize recursive sorting logic                 |
| No Loops Needed | Solves using pure recursive logic (no `for` or `while`) |
| Interview Prep  | Great for data structures & algorithms interviews       |

---

## 🔍 How Recursive Insertion Sort Works

1. Start from index `1`.
2. Recursively sort the first `n-1` elements.
3. Insert the `nth` element into the sorted subarray using recursion.

---

## ✅ Java Code – Recursive Insertion Sort

```java
public class Main {

    // Recursive function to sort array[0...n-1]
    public static void recursiveInsertionSort(int[] arr, int n) {
        // Base case
        if (n <= 1) return;

        // Sort first n-1 elements
        recursiveInsertionSort(arr, n - 1);

        // Insert last element at its correct position
        int last = arr[n - 1];
        int j = n - 2;

        // Move elements one step ahead to insert last element
        while (j >= 0 && arr[j] > last) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = last;
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 4, 1, 2};
        recursiveInsertionSort(arr, arr.length);

        for (int val : arr) {
            System.out.print(val + " ");
        }
    }
}
```

---

## 🖼️ Recursive Flow Diagram

Let's sort:
`arr = [5, 3, 4, 1, 2]`

```
recursiveInsertionSort(arr, 5)
 └── recursiveInsertionSort(arr, 4)
      └── recursiveInsertionSort(arr, 3)
           └── recursiveInsertionSort(arr, 2)
                └── recursiveInsertionSort(arr, 1) → base case

Insert 3 into [5] → [3, 5]
Insert 4 into [3, 5] → [3, 4, 5]
Insert 1 into [3, 4, 5] → [1, 3, 4, 5]
Insert 2 into [1, 3, 4, 5] → [1, 2, 3, 4, 5]
```

---

## 📊 Dry Run Table

| Step | Sorted Part    | Element Inserted | Resulting Array   |
| ---- | -------------- | ---------------- | ----------------- |
| 1    | `[5]`          | 3                | `[3, 5]`          |
| 2    | `[3, 5]`       | 4                | `[3, 4, 5]`       |
| 3    | `[3, 4, 5]`    | 1                | `[1, 3, 4, 5]`    |
| 4    | `[1, 3, 4, 5]` | 2                | `[1, 2, 3, 4, 5]` |

---

## 🧮 Time & Space Complexity

### Time Complexity

| Case    | Explanation                                     | Complexity |
| ------- | ----------------------------------------------- | ---------- |
| Best    | Already sorted, no shifts needed                | O(n)       |
| Average | Inserts and shifts every element                | O(n²)      |
| Worst   | Reverse sorted array (max shifts per insertion) | O(n²)      |

### Space Complexity

* **Auxiliary Stack Space**: `O(n)` due to recursion
* **In-place Sorting**: No additional array used → `O(1)` extra space

---

## 📌 Summary Table

| Concept       | Explanation                                   |
| ------------- | --------------------------------------------- |
| Method        | Recursively sort `n-1` and insert last        |
| Base Case     | When `n <= 1`, array is trivially sorted      |
| Stability     | ✅ Yes, maintains original order of duplicates |
| In-Place      | ✅ Yes, sorts without extra space              |
| Best Use Case | Small or nearly sorted datasets               |

---

## 🧾 Output

For input:

```java
int[] arr = {5, 3, 4, 1, 2};
```

Output:


1 2 3 4 5
