# Reverse the Array

In this problem, we reverse an array by swapping elements from the start (**L pointer**) and the end (**R pointer**) until the two pointers meet or cross each other.  
![rev arr](https://github.com/user-attachments/assets/df5ea5ee-638b-443e-8dd0-0ee14a5920a8)


)

## Key Points:
- The **L pointer** moves forward (left to right), and the **R pointer** moves backward (right to left).
- Swap the elements at these pointers: `arr[L] = arr[R]`.
- - Repeat the process until the boundary condition is met.

### Boundary Condition:
If the **L pointer** is greater than or equal to the **R pointer**, stop the process:
```java
if (L >= R) {
    return;
}
```

---

## Example:

**Initial Array:**  
`[1, 2, 3, 4, 5, 6]`

- **Step 1:**  
  Swap elements at L = 0, R = 5:  
  `[6, 2, 3, 4, 5, 1]`

- **Step 2:**  
  Swap elements at L = 1, R = 4:  
  `[6, 5, 3, 4, 2, 1]`

- **Step 3:**  
  Swap elements at L = 2, R = 3:  
  `[6, 5, 4, 3, 2, 1]`

Now, L = 3, R = 2, so the pointers have crossed, and the process stops.

**Reversed Array:**  
`[6, 5, 4, 3, 2, 1]`

---

## Java Code:
Here is the Java implementation for reversing an array using recursion:

```java
class Solution {
    // Function to reverse the array
    public void reverseArray(int arr[]) {
        // Start recursion with pointers at the ends
        rev(arr, arr.length - 1, 0);
    }

    // Recursive function to reverse the array
    public void rev(int arr[], int r, int l) {
        // Base condition: stop if L pointer crosses or meets R pointer
        if (l >= r) {
            return;
        }

        // Swap elements at L and R pointers
        int temp = arr[l];
        arr[l] = arr[r];
        arr[r] = temp;

        // Move the pointers
        rev(arr, r - 1, l + 1);
    }
}
```

---

## How It Works:
1. The function `reverseArray` starts the recursion by calling `rev(arr, arr.length - 1, 0)`:
   - `r` is the index of the last element.
   - `l` is the index of the first element.

2. The function `rev` swaps the elements at the `l` and `r` pointers.

3. The pointers are moved closer:
   - `l` is incremented by 1.
   - `r` is decremented by 1.

4. The recursion stops when `l >= r`.

---

## Test Case:

```java
public class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();

        // Input array
        int arr[] = {1, 2, 3, 4, 5, 6};

        System.out.println("Original Array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();

        // Reverse the array
        obj.reverseArray(arr);

        System.out.println("Reversed Array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

## Output:

**Original Array:**  
`1 2 3 4 5 6`  

**Reversed Array:**  
`6 5 4 3 2 1`

---
