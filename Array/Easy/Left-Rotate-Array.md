# 🔁 Left Rotate Array by One — Java Study Guide

---

## ✅ Problem Statement

> Given an array, rotate it **left by one position**.

Example:

```java
Input:  [1, 2, 3, 4]
Output: [2, 3, 4, 1]
```

---

## ⚙️ Brute Force Approach (Using Extra Array)

```java
public class Main {
    public static void bruteLeftRotateByOne(int[] array) {
        int[] temp = new int[array.length];

        for (int i = 1; i < array.length; i++) {
            temp[i - 1] = array[i];  // Shift all elements one step left
        }
        temp[array.length - 1] = array[0];  // Move first to last

        for (int i = 0; i < array.length; i++) {
            System.out.print(temp[i] + " ");
        }
    }

    public static void main(String[] args) {
        int array[] = {1, 2, 3, 4};
        bruteLeftRotateByOne(array);
    }
}
```

### 🔍 Dry Run

Input: `[1, 2, 3, 4]`
Temp after shifting: `[2, 3, 4, 0]`
Temp after adding first element at end: `[2, 3, 4, 1]`

---

## 🛠 Better Approach (Manual Shift in Same Array)

```java
public class Main {
    public static void betterLeftRotateByOne(int[] array) {
        int temp = array[0];
        for (int i = 0; i < array.length - 1; i++) {
            array[i] = array[i + 1];  // Shift elements left
        }
        array[array.length - 1] = temp;  // Add first at end

        for (int num : array) {
            System.out.print(num + " ");
        }
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4};
        betterLeftRotateByOne(array);
    }
}
```

### ⚡ Output:

```
2 3 4 1
```

---

## 🚀 Optimal (General) Approach – For Rotating by `k` Positions

This uses **reversal algorithm** (Best for large `k`):

```java
import java.util.*;

public class Main {
    public static void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++; end--;
        }
    }

    public static void rotateByK(int[] arr, int k) {
        int n = arr.length;
        k = k % n; // handle k > n

        reverse(arr, 0, k - 1);       // Step 1
        reverse(arr, k, n - 1);       // Step 2
        reverse(arr, 0, n - 1);       // Step 3

        for (int num : arr) {
            System.out.print(num + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        rotateByK(arr, 1);  // rotate left by 1
    }
}
```

✅ Output:

```
2 3 4 5 1
```

---

## 📊 Time & Space Complexity

| Approach           | Time | Space |
| ------------------ | ---- | ----- |
| Brute Force        | O(n) | O(n)  |
| Better (Shift)     | O(n) | O(1)  |
| Optimal (Reversal) | O(n) | O(1)  |

---

## 🧠 Visual Explanation

### Before Rotation

```
[1, 2, 3, 4]
 ^ first to move
```

### After Shift

```
[2, 3, 4, 1]
```

---

## 🧪 Try It Yourself (Custom Input)

Change this in main:

```java
int[] arr = {10, 20, 30, 40, 50};
rotateByK(arr, 1);  // Try with 2 or 3
```

---

## 💬 Summary

| Concept        | Key Point                     |
| -------------- | ----------------------------- |
| Left Rotation  | First element moves to last   |
| Right Rotation | Last element moves to first   |
| Best Approach  | Reversal method for large `k` |
