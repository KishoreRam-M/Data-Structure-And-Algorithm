# 🔄 Array Rotation: Left & Right by D Places (The Masterclass)

## 1\. Core Problem Definition: What is Array Rotation?

Imagine you have a queue of people, and some people from the front need to move to the back, or vice-versa. That's essentially array rotation\!

**Array Rotation** means rearranging the elements of an array such that some elements from one end are shifted to the other end.

  * **Left Rotation:** Elements from the beginning move to the end.
  * **Right Rotation:** Elements from the end move to the beginning.

**Key Terms:**

  * `arr`: The input array.
  * `N`: The total number of elements in the array (`arr.length`).
  * `D` (or `K`): The number of positions by which to rotate.

-----

## 2\. Helper Function: `reverse(arr, start, end)`

Before we dive into the optimal solution, let's define a small helper function that's super useful for in-place array manipulation, especially for the reversal algorithm.

This function simply reverses the elements within a specified range `[start, end]` (inclusive) of an array.

```java
// Helper function to reverse a portion of an array
private static void reverse(int[] arr, int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}
```

-----

## Part A: Left Array Rotation by D Places

**Problem:** Given an array `arr` of size `N` and an integer `D`, rotate the array `arr` to the left by `D` positions.

**Example:**
`arr = [1, 2, 3, 4, 5]`
`N = 5`
`D = 2` (Rotate left by 2 positions)

**Expected Output:** `[3, 4, 5, 1, 2]`

-----

### Approach 1: Brute-Force Method (Rotate One by One)

This is the most straightforward, intuitive approach.

1.  **Concept:** To rotate an array by `D` positions, we simply perform the "rotate by one position" operation `D` times.

2.  **How it Works (Step-by-Step):**

      * **Outer Loop:** Runs `D` times. Each iteration performs one left rotation.
      * **Inner Logic (Rotate by 1):**
          * Store the very first element (`arr[0]`) in a temporary variable (`temp`).
          * Shift every other element one position to the left (`arr[i] = arr[i+1]` for `i` from `0` to `N-2`).
          * Place the `temp` element (the original `arr[0]`) at the last position (`arr[N-1]`).

3.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `[ 1 | 2 | 3 | 4 | 5 ]`

    **Iteration 1 (Rotate by 1):**

      * `temp = 1`
      * Shift: `[ 2 | 3 | 4 | 5 | _ ]`
      * Place `temp`: `[ 2 | 3 | 4 | 5 | 1 ]`

    **Iteration 2 (Rotate by 1):**

      * `temp = 2`
      * Shift: `[ 3 | 4 | 5 | 1 | _ ]`
      * Place `temp`: `[ 3 | 4 | 5 | 1 | 2 ]`

    **Final Array:** `[ 3 | 4 | 5 | 1 | 2 ]`

4.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class LeftRotationBruteForce {

        public static void rotateLeftBruteForce(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return; // No rotation needed for empty, single-element, or D=0 array
            }
            d = d % n; // Normalize D: Rotating D times is same as rotating D % N times
            if (d == 0) {
                return; // After normalization, if d becomes 0, no effective rotation
            }
            // --- End Edge Case Handling ---

            // Outer loop: Repeat 'd' times for 'd' individual left rotations
            for (int i = 0; i < d; i++) {
                int temp = arr[0]; // Store the first element to be moved to the end

                // Inner loop: Shift all elements from index 1 to N-1, one position to the left
                for (int j = 0; j < n - 1; j++) {
                    arr[j] = arr[j + 1]; // Move element from right to left
                }

                arr[n - 1] = temp; // Place the stored element at the last position
            }
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateLeftBruteForce(arr1, 2);
            System.out.println("Left Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateLeftBruteForce(arr2, 3);
            System.out.println("Left Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]

            int[] arr3 = {7}; // Edge case: single element
            System.out.println("Original: " + Arrays.toString(arr3));
            rotateLeftBruteForce(arr3, 5);
            System.out.println("Left Rotated (D=5): " + Arrays.toString(arr3)); // Expected: [7]

            int[] arr4 = {1, 2, 3, 4, 5}; // Edge case: D > N
            System.out.println("Original: " + Arrays.toString(arr4));
            rotateLeftBruteForce(arr4, 7); // 7 % 5 = 2, same as D=2
            System.out.println("Left Rotated (D=7): " + Arrays.toString(arr4)); // Expected: [3, 4, 5, 1, 2]
        }
    }
    ```

5.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N \* D)**
          * The outer loop runs `D` times.
          * The inner loop (shifting) runs `N-1` times for each rotation.
          * In the worst case (when `D` is close to `N`), this approaches `O(N^2)`.
      * **Space Complexity: O(1)**
          * We only use a single `temp` variable, which is constant space.

6.  **Strengths and Weaknesses:**

      * **Strengths:** Very easy to understand and implement.
      * **Weaknesses:** Highly inefficient for large arrays or large rotation counts. Will likely cause "Time Limit Exceeded" (TLE) in coding contests for larger inputs.

-----

### Approach 2: Better Method (Using a Temporary Array)

This approach improves time complexity significantly by using a little extra memory.

1.  **Concept:** Instead of moving one element at a time, we store the `D` elements that need to be rotated in a separate temporary array. Then, we shift the remaining `N-D` elements to the front, and finally, place the stored `D` elements at the end.

2.  **How it Works (Step-by-Step):**

      * **Step 1: Store first `D` elements.** Create a `tempArr` of size `D`. Copy `arr[0]` to `arr[D-1]` into `tempArr`.
      * **Step 2: Shift remaining elements.** Move elements from `arr[D]` to `arr[N-1]` to the beginning of `arr` (i.e., to `arr[0]` to `arr[N-D-1]`).
      * **Step 3: Place stored elements.** Copy elements from `tempArr` back into `arr`, starting from index `N-D` to `N-1`.

3.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `arr: [ 1 | 2 | 3 | 4 | 5 ]`
    `N = 5, D = 2`

    **Step 1: Copy first D elements to `tempArr`**
    `tempArr: [ 1 | 2 ]`
    `arr:     [ 1 | 2 | 3 | 4 | 5 ]`

    **Step 2: Shift remaining (N-D) elements to the front**
    Elements `arr[2]` to `arr[4]` (i.e., `3, 4, 5`) move to `arr[0]` to `arr[2]`.
    `arr:     [ 3 | 4 | 5 | _ | _ ]`

    **Step 3: Copy `tempArr` back to the end**
    Elements from `tempArr` (i.e., `1, 2`) move to `arr[3]` to `arr[4]`.
    `arr:     [ 3 | 4 | 5 | 1 | 2 ]`

    **Final Output:** `[3, 4, 5, 1, 2]`

4.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class LeftRotationTempArray {

        public static void rotateLeftTempArray(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return;
            }
            d = d % n;
            if (d == 0) {
                return;
            }
            // --- End Edge Case Handling ---

            // Step 1: Create temp array and copy first 'd' elements
            int[] tempArr = new int[d];
            for (int i = 0; i < d; i++) {
                tempArr[i] = arr[i];
            }

            // Step 2: Shift remaining (N-D) elements to the front
            // Elements from index 'd' to 'n-1' move to '0' to 'n-d-1'
            for (int i = d; i < n; i++) {
                arr[i - d] = arr[i];
            }

            // Step 3: Copy elements from tempArr back to the end
            // Elements from tempArr[0] to tempArr[d-1] move to arr[n-d] to arr[n-1]
            for (int i = 0; i < d; i++) {
                arr[n - d + i] = tempArr[i];
            }
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateLeftTempArray(arr1, 2);
            System.out.println("Left Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateLeftTempArray(arr2, 3);
            System.out.println("Left Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]
        }
    }
    ```

5.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N)**
          * Each of the three steps involves a single pass over a part of the array. Total operations are proportional to `N` (e.g., `D + (N-D) + D = N+D`, which is `O(N)` since `D <= N`).
      * **Space Complexity: O(D)**
          * We use a `tempArr` of size `D`. In the worst case, `D` can be `N-1`, so it's effectively `O(N)` space.

6.  **Strengths and Weaknesses:**

      * **Strengths:** Much faster than brute-force (linear time). Generally acceptable in interviews if `O(1)` space is not strictly required.
      * **Weaknesses:** Uses extra space proportional to `D`. For extremely large arrays where memory is a critical constraint, this might not be optimal.

-----

### Approach 3: Optimal Method (Reversal Algorithm)

This is the most elegant and efficient solution, achieving both optimal time and space complexity. This is the one interviewers love to see\!

1.  **Concept:** The magic of this approach lies in three strategic reversals of array segments.
    If the array is conceptually divided into two parts: `A` (first `D` elements) and `B` (remaining `N-D` elements), then a left rotation transforms `[ A | B ]` into `[ B | A ]`.

    The steps are:

    1.  Reverse `A` (the first `D` elements). Array becomes `[ A^R | B ]`.
    2.  Reverse `B` (the remaining `N-D` elements). Array becomes `[ A^R | B^R ]`.
    3.  Reverse the entire array `[ A^R | B^R ]`. This results in `[ (A^R B^R)^R ]`, which mathematically simplifies to `[ B | A ]`.

2.  **Real-Life Analogy for Reversal Logic:**
    Imagine you have a long train with two sections: **Engine (A)** and **Carriages (B)**. You want to move the Engine to the back.

      * **Original:** `[Engine | Carriages]`
      * **Step 1: Reverse the Engine (A^R):** Imagine the engine itself turns around. `[Engine_Reversed | Carriages]`
      * **Step 2: Reverse the Carriages (B^R):** Now the carriages also turn around. `[Engine_Reversed | Carriages_Reversed]`
      * **Step 3: Reverse the Whole Train:** Now, reverse the entire train from end to end. The `Carriages_Reversed` will now be at the front and facing forward, and `Engine_Reversed` will be at the back and facing forward.
        `[Carriages | Engine]` - Exactly what we wanted\!

3.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `arr: [ 1 | 2 | 3 | 4 | 5 ]`
    `N = 5, D = 2`
    `A = [1, 2]`, `B = [3, 4, 5]`

    **Step 1: Reverse first `D` elements (from index 0 to `D-1`)**
    `reverse(arr, 0, 1)`: Reverse `[1, 2]` to `[2, 1]`
    `arr: [ 2 | 1 | 3 | 4 | 5 ]`

    **Step 2: Reverse remaining `N-D` elements (from index `D` to `N-1`)**
    `reverse(arr, 2, 4)`: Reverse `[3, 4, 5]` to `[5, 4, 3]`
    `arr: [ 2 | 1 | 5 | 4 | 3 ]`

    **Step 3: Reverse the entire array (from index 0 to `N-1`)**
    `reverse(arr, 0, 4)`: Reverse `[2, 1, 5, 4, 3]` to `[3, 4, 5, 1, 2]`
    `arr: [ 3 | 4 | 5 | 1 | 2 ]`

    **Final Output:** `[3, 4, 5, 1, 2]`

4.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class LeftRotationOptimal {

        // Helper function (defined earlier)
        private static void reverse(int[] arr, int start, int end) {
            while (start < end) {
                int temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                start++;
                end--;
            }
        }

        public static void rotateLeftOptimal(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return;
            }
            d = d % n; // Normalize D
            if (d == 0) {
                return;
            }
            // --- End Edge Case Handling ---

            // Step 1: Reverse the first 'd' elements (from index 0 to d-1)
            reverse(arr, 0, d - 1);

            // Step 2: Reverse the remaining 'n-d' elements (from index d to n-1)
            reverse(arr, d, n - 1);

            // Step 3: Reverse the entire array (from index 0 to n-1)
            reverse(arr, 0, n - 1);
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateLeftOptimal(arr1, 2);
            System.out.println("Left Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateLeftOptimal(arr2, 3);
            System.out.println("Left Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]
        }
    }
    ```

5.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N)**
          * Each `reverse` call takes `O(length_of_segment)` time. Since we reverse segments that sum up to `N` (or less), the total time is proportional to `N`. Specifically, `O(D) + O(N-D) + O(N) = O(N)`.
      * **Space Complexity: O(1)**
          * All operations are done in-place, using only a few constant variables.

6.  **Strengths and Weaknesses:**

      * **Strengths:** Optimal in both time (`O(N)`) and space (`O(1)`) complexity. This is the most efficient solution.
      * **Weaknesses:** The logic might not be immediately intuitive without understanding the `(A^R B^R)^R = BA` mathematical property. Requires careful indexing for the `reverse` calls.

-----

## Part B: Right Array Rotation by D Places

**Problem:** Given an array `arr` of size `N` and an integer `D`, rotate the array `arr` to the **right** by `D` positions.

**Example:**
`arr = [1, 2, 3, 4, 5]`
`N = 5`
`D = 2` (Rotate right by 2 positions)

**Expected Output:** `[4, 5, 1, 2, 3]`

-----

### Key Insight: Right Rotation as Left Rotation

The simplest way to think about right rotation is to convert it into an equivalent left rotation.
Rotating an array to the **right by `D` positions** is equivalent to rotating it to the **left by `N - D` positions**.

**Example:** `arr = [1, 2, 3, 4, 5]`, `N=5`, Right `D=2`
Equivalent Left Rotation `D_left = N - D = 5 - 2 = 3`.
So, we can just call our `rotateLeftOptimal(arr, 3)` function.

`[1,2,3,4,5]` -\> Left by 3 -\> `[4,5,1,2,3]` (Correct\!)

-----

### Approach 1: Brute-Force Method (Right Rotate One by One)

1.  **Concept:** Similar to left brute-force, but we move the *last* element to the *first* position, `D` times.

2.  **How it Works (Step-by-Step):**

      * **Outer Loop:** Runs `D` times. Each iteration performs one right rotation.
      * **Inner Logic (Rotate by 1):**
          * Store the very last element (`arr[N-1]`) in a temporary variable (`temp`).
          * Shift every other element one position to the right (`arr[i] = arr[i-1]` for `i` from `N-1` down to `1`).
          * Place the `temp` element (the original `arr[N-1]`) at the first position (`arr[0]`).

3.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `[ 1 | 2 | 3 | 4 | 5 ]`

    **Iteration 1 (Rotate by 1):**

      * `temp = 5`
      * Shift: `[ _ | 1 | 2 | 3 | 4 ]`
      * Place `temp`: `[ 5 | 1 | 2 | 3 | 4 ]`

    **Iteration 2 (Rotate by 1):**

      * `temp = 4`
      * Shift: `[ _ | 5 | 1 | 2 | 3 ]`
      * Place `temp`: `[ 4 | 5 | 1 | 2 | 3 ]`

    **Final Array:** `[ 4 | 5 | 1 | 2 | 3 ]`

4.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class RightRotationBruteForce {

        public static void rotateRightBruteForce(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return;
            }
            d = d % n; // Normalize D
            if (d == 0) {
                return;
            }
            // --- End Edge Case Handling ---

            // Outer loop: Repeat 'd' times for 'd' individual right rotations
            for (int i = 0; i < d; i++) {
                int temp = arr[n - 1]; // Store the last element to be moved to the front

                // Inner loop: Shift all elements from index N-2 down to 0, one position to the right
                for (int j = n - 1; j > 0; j--) {
                    arr[j] = arr[j - 1]; // Move element from left to right
                }

                arr[0] = temp; // Place the stored element at the first position
            }
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateRightBruteForce(arr1, 2);
            System.out.println("Right Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [4, 5, 1, 2, 3]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateRightBruteForce(arr2, 3);
            System.out.println("Right Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]
        }
    }
    ```

5.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N \* D)** (Same as Left Brute-Force)
      * **Space Complexity: O(1)** (Same as Left Brute-Force)

-----

### Approach 2: Better Method (Right Rotation Using Temporary Array)

1.  **Concept:** Store the *last* `D` elements in a temporary array. Shift the first `N-D` elements to the right. Then place the stored `D` elements at the beginning.

2.  **How it Works (Step-by-Step):**

      * **Step 1: Store last `D` elements.** Create a `tempArr` of size `D`. Copy `arr[N-D]` to `arr[N-1]` into `tempArr`.
      * **Step 2: Shift first `N-D` elements.** Move elements from `arr[0]` to `arr[N-D-1]` to the right, starting from `arr[N-1]` down to `arr[D]`.
      * **Step 3: Place stored elements.** Copy elements from `tempArr` back into `arr`, starting from index `0` to `D-1`.

3.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `arr: [ 1 | 2 | 3 | 4 | 5 ]`
    `N = 5, D = 2`

    **Step 1: Copy last D elements to `tempArr`**
    `tempArr: [ 4 | 5 ]`
    `arr:     [ 1 | 2 | 3 | 4 | 5 ]`

    **Step 2: Shift first (N-D) elements to the right**
    Elements `arr[0]` to `arr[2]` (i.e., `1, 2, 3`) move to `arr[2]` to `arr[4]`.
    `arr:     [ _ | _ | 1 | 2 | 3 ]`

    **Step 3: Copy `tempArr` back to the beginning**
    Elements from `tempArr` (i.e., `4, 5`) move to `arr[0]` to `arr[1]`.
    `arr:     [ 4 | 5 | 1 | 2 | 3 ]`

    **Final Output:** `[4, 5, 1, 2, 3]`

4.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class RightRotationTempArray {

        public static void rotateRightTempArray(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return;
            }
            d = d % n; // Normalize D
            if (d == 0) {
                return;
            }
            // --- End Edge Case Handling ---

            // Step 1: Create temp array and copy last 'd' elements
            int[] tempArr = new int[d];
            for (int i = 0; i < d; i++) {
                tempArr[i] = arr[n - d + i];
            }

            // Step 2: Shift first (N-D) elements to the right
            // Elements from index 'n-d-1' down to '0' move to 'n-1' down to 'd'
            for (int i = n - d - 1; i >= 0; i--) {
                arr[i + d] = arr[i];
            }

            // Step 3: Copy elements from tempArr back to the beginning
            // Elements from tempArr[0] to tempArr[d-1] move to arr[0] to arr[d-1]
            for (int i = 0; i < d; i++) {
                arr[i] = tempArr[i];
            }
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateRightTempArray(arr1, 2);
            System.out.println("Right Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [4, 5, 1, 2, 3]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateRightTempArray(arr2, 3);
            System.out.println("Right Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]
        }
    }
    ```

5.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N)** (Same as Left Temp Array)
      * **Space Complexity: O(D)** (Same as Left Temp Array)

-----

### Approach 3: Optimal Method (Right Rotation Using Reversal Algorithm)

1.  **Concept:** Similar to left rotation, but the order of reversals changes.
    If the array is `[ A | B ]` where `A` is the first `N-D` elements and `B` is the last `D` elements, a right rotation transforms `[ A | B ]` into `[ B | A ]`.

    The steps are:

    1.  Reverse `A` (the first `N-D` elements). Array becomes `[ A^R | B ]`.
    2.  Reverse `B` (the last `D` elements). Array becomes `[ A^R | B^R ]`.
    3.  Reverse the entire array `[ A^R | B^R ]`. This results in `[ (A^R B^R)^R ]`, which mathematically simplifies to `[ B | A ]`.

2.  **Visual Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`**

    **Initial Array:**
    `arr: [ 1 | 2 | 3 | 4 | 5 ]`
    `N = 5, D = 2`
    `A = [1, 2, 3]` (first N-D = 3 elements), `B = [4, 5]` (last D = 2 elements)

    **Step 1: Reverse first `N-D` elements (from index 0 to `N-D-1`)**
    `reverse(arr, 0, 2)`: Reverse `[1, 2, 3]` to `[3, 2, 1]`
    `arr: [ 3 | 2 | 1 | 4 | 5 ]`

    **Step 2: Reverse last `D` elements (from index `N-D` to `N-1`)**
    `reverse(arr, 3, 4)`: Reverse `[4, 5]` to `[5, 4]`
    `arr: [ 3 | 2 | 1 | 5 | 4 ]`

    **Step 3: Reverse the entire array (from index 0 to `N-1`)**
    `reverse(arr, 0, 4)`: Reverse `[3, 2, 1, 5, 4]` to `[4, 5, 1, 2, 3]`
    `arr: [ 4 | 5 | 1 | 2 | 3 ]`

    **Final Output:** `[4, 5, 1, 2, 3]`

3.  **Java Code Implementation:**

    ```java
    import java.util.Arrays;

    public class RightRotationOptimal {

        // Helper function (defined earlier)
        private static void reverse(int[] arr, int start, int end) {
            while (start < end) {
                int temp = arr[start];
                arr[start] = arr[end];
                arr[end] = temp;
                start++;
                end--;
            }
        }

        public static void rotateRightOptimal(int[] arr, int d) {
            int n = arr.length;

            // --- Edge Case Handling & Normalization ---
            if (n == 0 || d == 0 || n == 1) {
                return;
            }
            d = d % n; // Normalize D
            if (d == 0) {
                return;
            }
            // --- End Edge Case Handling ---

            // Step 1: Reverse the first (N-D) elements (from index 0 to N-D-1)
            reverse(arr, 0, n - d - 1);

            // Step 2: Reverse the last 'd' elements (from index N-D to N-1)
            reverse(arr, n - d, n - 1);

            // Step 3: Reverse the entire array (from index 0 to n-1)
            reverse(arr, 0, n - 1);
        }

        public static void main(String[] args) {
            int[] arr1 = {1, 2, 3, 4, 5};
            System.out.println("Original: " + Arrays.toString(arr1));
            rotateRightOptimal(arr1, 2);
            System.out.println("Right Rotated (D=2): " + Arrays.toString(arr1)); // Expected: [4, 5, 1, 2, 3]

            int[] arr2 = {10, 20, 30, 40, 50, 60};
            System.out.println("Original: " + Arrays.toString(arr2));
            rotateRightOptimal(arr2, 3);
            System.out.println("Right Rotated (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]
        }
    }
    ```

4.  **Time and Space Complexity Analysis:**

      * **Time Complexity: O(N)** (Optimal)
      * **Space Complexity: O(1)** (Optimal)

-----

## 3\. Common Mistakes & How to Avoid Them (Consolidated)

These apply to all approaches:

1.  **Not Normalizing `D` (`d = d % n;`)**:
      * **Mistake:** If `D` is larger than `N` (e.g., rotating a 5-element array by 7 positions), and you don't use `d = d % n;`, your code will perform unnecessary rotations or even go out of bounds.
      * **Avoid:** ALWAYS add `d = d % n;` at the beginning of your rotation function. This ensures `D` is always within `[0, N-1]`. If `d` becomes `0` after normalization, it means no effective rotation, so you can `return`.
2.  **Off-by-One Errors in Loop Bounds/Indices:**
      * **Mistake:** Using `N-1` instead of `N` or vice-versa, or incorrect `start`/`end` indices for `reverse` calls. This is *very* common.
      * **Avoid:** Carefully trace your loops and `reverse` calls on paper with small examples. Pay attention to `inclusive` vs. `exclusive` bounds. For `reverse(arr, start, end)`, `start` and `end` are usually *inclusive*.
3.  **Not Handling Edge Cases (`N=0`, `D=0`, `N=1`):**
      * **Mistake:** Assuming the array will always have multiple elements or `D` will always be positive.
      * **Avoid:** Add initial checks: `if (n == 0 || d == 0 || n == 1) return;`. This makes your code robust.
4.  **Modifying Array While Iterating (Brute-Force Inner Loop):**
      * **Mistake:** If you're not careful with `temp` variable in brute-force, you might overwrite elements before they are used.
      * **Avoid:** Ensure `temp` holds the value that needs to be preserved before shifting.

-----

## 4\. Interview Perspective: Google, Amazon, Flipkart

Companies like Google, Amazon, and Flipkart often ask array rotation problems because they test:

  * **Problem-Solving Progression:** Can you start with a simple idea and optimize it?
  * **Understanding Constraints:** Do you consider time and space complexity?
  * **Edge Case Handling:** Do you write robust code that doesn't break for unusual inputs?
  * **Code Quality:** Is your code clean, readable, and well-commented?
  * **Communication:** Can you explain your thought process clearly, articulate trade-offs, and justify your chosen approach?

**How they ask:**

  * "Rotate an array to the left by K positions." (Most common)
  * "Rotate an array to the right by K positions."
  * "Given an array, check if it's a rotated version of another array." (Often involves finding the pivot point or sorting and comparing).
  * "Find an element in a rotated sorted array." (Binary search variant).

**What they look for:**

1.  **Start with Brute-Force:** "Okay, a simple way would be to rotate one by one..." (Explain `O(N*D)` time, `O(1)` space). This shows you can solve it, even if inefficiently.
2.  **Optimize with Temp Array:** "This is too slow for large inputs, so we can optimize using a temporary array..." (Explain `O(N)` time, `O(D)` space). This shows you understand efficiency.
3.  **Present Optimal Solution:** "For an even more optimal solution, we can use the reversal algorithm..." (Explain `O(N)` time, `O(1)` space). This truly sets you apart.
4.  **Dry Run:** Be ready to dry run any of your chosen solutions with a small example on the whiteboard.
5.  **Edge Cases:** Discuss how you'd handle `D=0`, `D=N`, `D>N`, empty array, single element array.
6.  **Right Rotation:** If asked for left, be prepared to explain how to adapt for right (and vice-versa).
7.  **Clear Communication:** Speak out your thoughts, explain variable names, and justify decisions.

-----

## 5\. Extending to Other Data Structures

The core idea of rotation can be adapted, but the implementation changes significantly based on the data structure.

### 5.1. 2D Arrays (Matrix Rotation)

  * **Concept:** This usually means rotating the entire matrix by 90, 180, or 270 degrees clockwise/counter-clockwise. It's not about shifting elements linearly but about changing their `(row, col)` positions.
  * **Difference:** Not a direct application of the 1D array rotation algorithms. It involves:
      * **Transposing the matrix:** Swapping elements across the main diagonal (`arr[i][j]` becomes `arr[j][i]`).
      * **Reversing rows/columns:** After transpose, you reverse rows (for 90-degree clockwise) or columns (for 90-degree counter-clockwise).
  * **Complexity:** Typically `O(N*M)` time (where N, M are dimensions) and `O(1)` space (in-place).

### 5.2. Linked Lists

  * **Concept:** Rotating a linked list means moving the `D` first nodes to the end of the list.
  * **Difference:** You don't have random access by index like arrays. You manipulate pointers (`next` references).
  * **How it Works (High-Level):**
    1.  Find the `D`-th node from the head (this will be the new tail of the first part).
    2.  Find the `(D+1)`-th node (this will be the new head).
    3.  Make the `D`-th node's `next` pointer `null` (to break the list).
    4.  Traverse to the original tail of the list.
    5.  Make the original tail's `next` pointer point to the original head.
    6.  The `(D+1)`-th node is now the new head.
  * **Complexity:** `O(N)` time (for traversal), `O(1)` space.

-----

## 6\. Quiz Questions (Test Your Understanding\!)

1.  Given `arr = [10, 20, 30, 40, 50, 60]`, what is the result of `rotateLeftOptimal(arr, 4)`?
2.  If `arr = [A, B, C, D]` and you call `rotateRightOptimal(arr, 6)`, what will be the final array?
3.  Which array rotation approach is best if you have extremely limited memory (e.g., embedded systems) but time is less critical?
4.  Explain why `d = d % n;` is important when `D` is larger than `N`.
5.  In the optimal left rotation, if `D = 0`, what happens in the `reverse` calls?

-----

## 7\. Debugging Scenarios

1.  **Issue:** Your brute-force left rotation code gives `[0, 0, 0, 0, 1]` for `[1, 2, 3, 4, 5], D=1`.
      * **Possible Cause:** Off-by-one error in the inner loop, possibly `arr[j+1]` is used for `arr[j]` but the loop range goes too far, overwriting elements with default `0` or going out of bounds. Or, `temp` is not correctly stored/used.
      * **Debugging Tip:** Use a debugger. Set a breakpoint at the start of the inner loop and step through, watching `arr` and `temp` values.
2.  **Issue:** Your optimal (reversal) left rotation code gives `[5, 4, 3, 2, 1]` for `[1, 2, 3, 4, 5], D=2`.
      * **Possible Cause:** You likely reversed the *entire* array first, or reversed the segments in the wrong order. The steps are specific: `(0, D-1)`, then `(D, N-1)`, then `(0, N-1)`.
      * **Debugging Tip:** Dry run on paper. Verify the `start` and `end` indices for each of the three `reverse` calls.

-----

## 8\. Practice Problems (Increasing Difficulty)

1.  **Easy:** Implement `rotateLeftOptimal` and `rotateRightOptimal` for a `char[]` array instead of `int[]`.
      * Input: `char[] arr = {'a', 'b', 'c', 'd', 'e'}; D = 3;`
      * Expected Left: `{'d', 'e', 'a', 'b', 'c'}`
2.  **Medium:** Given a sorted array that has been rotated an unknown number of times, find the minimum element in it. (Hint: This is a binary search problem, not direct rotation).
      * Input: `[4, 5, 6, 7, 0, 1, 2]`
      * Expected Output: `0`
3.  **Hard:** Implement a function to rotate a matrix (2D array) by 90 degrees clockwise in-place.
      * Input: `[[1, 2, 3], [4, 5, 6], [7, 8, 9]]`
      * Expected Output: `[[7, 4, 1], [8, 5, 2], [9, 6, 3]]`

-----

## 9\. Summary Comparison Table

| Feature          | Brute-Force (Rotate 1 by 1) | Better (Temp Array) | Optimal (Reversal Algorithm) |
| :--------------- | :-------------------------- | :------------------ | :--------------------------- |
| **Time Complexity** | O(N \* D)                    | O(N)                | O(N)                         |
| **Space Complexity** | O(1)                        | O(D) (or O(N))      | O(1)                         |
| **In-place?** | Yes                         | No (uses temp array)| Yes                          |
| **Ease of Understanding** | Very Easy                   | Easy                | Moderate (conceptually tricky)|
| **Pros** | Simplest to code            | Good time complexity| Optimal in both time & space |
| **Cons** | Very slow for large inputs  | Uses extra memory   | Less intuitive initially     |
| **Interview/CP Use** | Rarely (only as starting point) | Common, good fallback | **Highly Preferred** |
| **Left Rotation Logic** | Shift left, move first to end | Copy first D, shift, copy back | `reverse(0, D-1)`, `reverse(D, N-1)`, `reverse(0, N-1)` |
| **Right Rotation Logic** | Shift right, move last to start | Copy last D, shift, copy back | `reverse(0, N-D-1)`, `reverse(N-D, N-1)`, `reverse(0, N-1)` |
