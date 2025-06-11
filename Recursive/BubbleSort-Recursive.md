# 🔄 Recursive Bubble Sort – The Ultimate Guide

## ✳️ What is Bubble Sort?

**Bubble Sort** is a simple comparison-based sorting algorithm where each pair of adjacent elements is compared, and elements are swapped if they are in the wrong order. This process repeats until the array is sorted.

---

## ❓ Why Use Recursion in Bubble Sort?

| Purpose        | Explanation                                                        |
| -------------- | ------------------------------------------------------------------ |
| Learning       | Helps understand recursive thinking and call flow.                 |
| No Loops       | Useful in environments or exercises where loops are not allowed.   |
| Simulation     | Simulates nested loops using recursive calls.                      |
| Interview Prep | Excellent for strengthening your recursion concepts in interviews. |

---

## 🔁 Recursive vs Iterative Bubble Sort

| Feature        | Recursive Bubble Sort                   | Iterative Bubble Sort                       |
| -------------- | --------------------------------------- | ------------------------------------------- |
| Structure      | Uses recursive calls to simulate loops  | Uses nested loops                           |
| Readability    | Can be harder to read and debug         | Easier for beginners                        |
| Stack Overhead | Uses call stack memory                  | No extra stack memory                       |
| Use Case       | Conceptual learning, recursion practice | Practical applications, performance-focused |

---

## 🧠 How Recursive Bubble Sort Works

Recursive Bubble Sort uses **two recursive functions**:

1. **Outer Function** `bubbleSort(arr, n)`
   → Controls the number of passes
   → Shrinks the array range each pass (`n - 1`)

2. **Inner Function** `bubblePass(arr, i, n)`
   → Compares and swaps adjacent elements from `i` to `n - 2`

---

## ✅ Java Code for Recursive Bubble Sort

```java
public class Main {
    // Swap two elements
    public static void swap(int[] arr, int i) {
        int temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
    }

    // Inner recursive function to make one pass
    public static void bubblePass(int[] arr, int i, int n) {
        if (i == n - 1) return;
        if (arr[i] > arr[i + 1]) swap(arr, i);
        bubblePass(arr, i + 1, n);
    }

    // Outer recursive function
    public static void bubbleSort(int[] arr, int n) {
        if (n == 1) return;
        bubblePass(arr, 0, n);
        bubbleSort(arr, n - 1);
    }

    public static void main(String[] args) {
        int[] arr = {5, 1, 4, 2, 8};
        bubbleSort(arr, arr.length);
        for (int val : arr) System.out.print(val + " ");
    }
}
```

---

## 🖼️ Recursive Flow Diagram

Let's say:
**Input:** `arr = [5, 1, 4, 2, 8]`

### 🔃 Recursive Calls Breakdown

```text
bubbleSort(arr, 5)           ← Outer Pass 1
 └── bubblePass(arr, 0, 5)
     ├── compare 5 & 1 → swap → [1, 5, 4, 2, 8]
     ├── compare 5 & 4 → swap → [1, 4, 5, 2, 8]
     ├── compare 5 & 2 → swap → [1, 4, 2, 5, 8]
     └── compare 5 & 8 → OK

bubbleSort(arr, 4)           ← Outer Pass 2
 └── bubblePass(arr, 0, 4)
     ├── compare 1 & 4 → OK
     ├── compare 4 & 2 → swap → [1, 2, 4, 5, 8]
     └── compare 4 & 5 → OK

bubbleSort(arr, 3)           ← Outer Pass 3
 └── bubblePass(arr, 0, 3)
     ├── compare 1 & 2 → OK
     └── compare 2 & 4 → OK

bubbleSort(arr, 2)           ← Outer Pass 4
 └── bubblePass(arr, 0, 2)
     └── compare 1 & 2 → OK

bubbleSort(arr, 1) → base case, return
```

---

## 🔢 Dry Run Table

| Pass | Comparison Steps           | Resulting Array   |
| ---- | -------------------------- | ----------------- |
| 1    | 5>1 ✔, 5>4 ✔, 5>2 ✔, 5<8 ✖ | `[1, 4, 2, 5, 8]` |
| 2    | 1<4 ✖, 4>2 ✔, 4<5 ✖        | `[1, 2, 4, 5, 8]` |
| 3    | 1<2 ✖, 2<4 ✖               | `[1, 2, 4, 5, 8]` |
| 4    | 1<2 ✖                      | `[1, 2, 4, 5, 8]` |

---

## 🧮 Time & Space Complexity

### ⏱ Time Complexity

| Case    | Explanation                                          | Complexity |
| ------- | ---------------------------------------------------- | ---------- |
| Worst   | Every element compared with each other               | `O(n^2)`   |
| Average | Nested comparisons                                   | `O(n^2)`   |
| Best    | Still `O(n^2)` because recursion doesn’t skip passes | `O(n^2)`   |

> Recursive Bubble Sort **does not optimize** for already sorted arrays unless you modify it with a `swapped` flag.

---

### 🧠 Space Complexity

| Case  | Explanation                       | Complexity |
| ----- | --------------------------------- | ---------- |
| Stack | Each recursive call adds to stack | `O(n)`     |
| Array | Sorted in-place                   | `O(1)`     |

---

## 📘 Best Use Case

Recursive bubble sort is **not used in production** due to inefficiency. It is mainly used for:

* Teaching recursion
* Interview questions to test recursion skills
* Academic or conceptual clarity

---

## 🧾 Final Output

For input:

```java
int[] arr = {5, 1, 4, 2, 8};
```

Output:

```text
1 2 4 5 8
```

---

## 📌 Summary Table

| Aspect         | Recursive Bubble Sort Explanation                |
| -------------- | ------------------------------------------------ |
| Method         | Two recursive functions (outer and inner)        |
| Recursion Base | When length `n == 1`                             |
| Inner Flow     | Recursively compares and swaps till end of array |
| Outer Flow     | Shrinks unsorted range recursively               |
| Space          | `O(n)` (call stack)                              |
| Time           | `O(n^2)` in all cases unless optimized           |
| Advantage      | Strengthens recursion skills                     |
| Disadvantage   | Less efficient than other sorting algorithms     |
