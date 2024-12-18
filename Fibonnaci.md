# Fibonacci Series

The Fibonacci series is a sequence of numbers where each number is the sum of the two preceding ones, starting with `0` and `1`. Here's how it works:  
    ![fibonnaci](https://github.com/user-attachments/assets/9f8807ec-ecab-419d-bac0-f9e5601b8389)

**Fibonacci Sequence Example:**  
`0, 1, 1, 2, 3, 5, 8, 13, 21, ...`  

---

## **Boundary Conditions**
1. **For `n = 0`:**  
   If the input is `0`, the Fibonacci value is `0`.  
   **Code:**  
   ```java
   if (n == 0) {
       return 0; // Base case
   }
   ```

2. **For `n = 1`:**  
   If the input is `1`, the Fibonacci value is `1`.  
   **Code:**  
   ```java
   if (n == 1) {
       return 1; // Base case
   }
   ```

---

## **Java Code for Fibonacci Calculation**

Below is a simple recursive implementation of the Fibonacci series in Java:  

```java
class Solution {
    public int fib(int n) {
        if (n == 0) {
            return 0;  // Base case for fib(0)
        } else if (n == 1) {
            return 1;  // Base case for fib(1)
        } else {
            return fib(n - 1) + fib(n - 2);  // Recursive step
        }
    }
}
```

### **How It Works:**
- If the input `n` is `0` or `1`, the method directly returns the value.  
- For any other value of `n`, it recursively calculates `fib(n-1)` and `fib(n-2)` and returns their sum.  

---

## **Visual Representation**  
The recursive tree for `fib(4)` looks like this:

```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1) = 1
│   │   └── fib(0) = 0
│   └── fib(1) = 1
└── fib(2)
    ├── fib(1) = 1
    └── fib(0) = 0
```

This recursive structure calculates the Fibonacci numbers step by step.

---

### **Key Points:**
- Simple to implement but not efficient for large `n` due to repeated calculations.  
- For efficiency, consider using **dynamic programming** or **memoization**.  
