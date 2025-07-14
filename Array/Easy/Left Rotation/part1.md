# 🔄 Left Array Rotation by D Places: Your Complete Study Kit

## Problem Statement: What is Array Rotation?

Imagine you have a list of items, like numbers in an array. A **left rotation** means taking the first few elements from the beginning and moving them to the end of the array, shifting all other elements to the left.

**Formal Definition:** Given an array `arr` of size `N` and an integer `D`, rotate the array `arr` to the left by `D` positions.

**Example:**
`arr = [1, 2, 3, 4, 5]`
`N = 5`
`D = 2` (Rotate left by 2 positions)

**Expected Output:** `[3, 4, 5, 1, 2]`

**Use Cases:**

  * **Circular Buffers:** In system design, when you have a fixed-size buffer (like for logs or network packets), and new data comes in, old data "rotates out."
  * **Game Development:** Shifting elements in a game board or a character's inventory.
  * **Scheduling/Queues:** Managing tasks in a circular fashion.
  * **Data Processing:** Reordering data for specific algorithms or display.

-----

## Approach 1: Brute-Force Method (Rotate One by One)

This is the simplest idea that comes to mind first. It's like moving one person from the front of a line to the back, then repeating that `D` times.

### How it Works: Full Walkthrough

1.  **Repeat `D` times:** We need to perform the "rotate by one" operation `D` times.
2.  **Rotate by One:**
      * Store the first element of the array in a temporary variable (`temp`).
      * Shift all remaining elements one position to the left (e.g., `arr[i] = arr[i+1]`).
      * Place the `temp` element at the very end of the array (`arr[N-1] = temp`).

### Diagrams & Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`

**Initial:**
`arr: [ 1 | 2 | 3 | 4 | 5 ]`

**Rotation 1 (D=1):**

  * `temp = arr[0]` (which is `1`)
  * Shift elements left:
    `arr: [ 2 | 3 | 4 | 5 | _ ]`
  * Place `temp` at end:
    `arr: [ 2 | 3 | 4 | 5 | 1 ]`

**Rotation 2 (D=2):**

  * `temp = arr[0]` (which is `2`)
  * Shift elements left:
    `arr: [ 3 | 4 | 5 | 1 | _ ]`
  * Place `temp` at end:
    `arr: [ 3 | 4 | 5 | 1 | 2 ]`

**Final Output:** `[3, 4, 5, 1, 2]`

### Code Implementation: Pure Java

```java
import java.util.Arrays;

public class ArrayRotationBruteForce {

    /**
     * Rotates an array to the left by D positions using the brute-force method.
     * Time Complexity: O(N * D)
     * Space Complexity: O(1)
     *
     * @param arr The array to be rotated.
     * @param d The number of positions to rotate.
     */
    public static void rotateLeftBruteForce(int[] arr, int d) {
        int n = arr.length;

        // Handle edge cases: empty array, single element, or no rotation needed
        if (n == 0 || d == 0 || n == 1) {
            return;
        }

        // Normalize D: If D is greater than N, rotating D times is same as rotating D % N times.
        // This prevents unnecessary rotations and handles D = N (which means no effective rotation).
        d = d % n;
        if (d == 0) { // After normalization, if d becomes 0, no rotation needed.
            return;
        }

        // Outer loop: Repeat 'd' times for 'd' rotations
        for (int i = 0; i < d; i++) {
            int temp = arr[0]; // Store the first element

            // Inner loop: Shift all elements one position to the left
            for (int j = 0; j < n - 1; j++) {
                arr[j] = arr[j + 1];
            }

            arr[n - 1] = temp; // Place the stored element at the end
        }
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        System.out.println("Original Array 1: " + Arrays.toString(arr1));
        rotateLeftBruteForce(arr1, 2);
        System.out.println("Rotated Array 1 (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

        int[] arr2 = {10, 20, 30, 40, 50, 60};
        System.out.println("Original Array 2: " + Arrays.toString(arr2));
        rotateLeftBruteForce(arr2, 3);
        System.out.println("Rotated Array 2 (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]

        int[] arr3 = {7};
        System.out.println("Original Array 3: " + Arrays.toString(arr3));
        rotateLeftBruteForce(arr3, 5);
        System.out.println("Rotated Array 3 (D=5): " + Arrays.toString(arr3)); // Expected: [7] (D % N = 5 % 1 = 0)

        int[] arr4 = {};
        System.out.println("Original Array 4: " + Arrays.toString(arr4));
        rotateLeftBruteForce(arr4, 10);
        System.out.println("Rotated Array 4 (D=10): " + Arrays.toString(arr4)); // Expected: []
    }
}
```

### Time and Space Complexity Analysis

  * **Time Complexity: O(N \* D)**
      * The outer loop runs `D` times.
      * The inner loop (for shifting elements) runs `N-1` times in each iteration of the outer loop.
      * So, total operations roughly `D * N`.
      * *Example:* If `N=1000` and `D=500`, this is `500,000` operations. Not great for large inputs.
  * **Space Complexity: O(1)**
      * We only use a single `temp` variable, which is constant space regardless of `N` or `D`.

### Strengths and Weaknesses

  * **Strengths:**
      * **Simple to understand and implement.** Great for a quick, small-scale solution.
  * **Weaknesses:**
      * **Inefficient for large `N` or `D` values.** If `D` is close to `N`, it's almost `O(N^2)`.
      * Can lead to "Time Limit Exceeded" (TLE) in competitive programming.

### Edge Cases & Handling

  * **Empty Array (`N=0`):** Handled by `if (n == 0) return;`.
  * **Single Element Array (`N=1`):** Handled by `if (n == 1) return;` or `d = d % n;` (as `d % 1` will always be `0`).
  * **`D = 0`:** No rotation needed. Handled by `if (d == 0) return;`.
  * **`D = N`:** Rotating `N` times brings the array back to its original state. Handled by `d = d % n;` (as `N % N = 0`).
  * **`D > N`:** Rotating `D` times is equivalent to rotating `D % N` times. For example, rotating `[1,2,3,4,5]` by `7` is same as rotating by `7 % 5 = 2`. Handled by `d = d % n;`.

### Common Mistakes to Avoid

  * **Off-by-one errors:** Ensure inner loop runs `N-1` times and `arr[n-1]` is the correct placement for `temp`.
  * **Not normalizing `D`:** Forgetting `d = d % n;` can lead to unnecessary computations or incorrect results if `D` is very large.

-----

## Approach 2: Better Method (Using a Temporary Array)

This approach is much more efficient in terms of time complexity by sacrificing a bit of space. It's like taking the first `D` people, putting them aside, letting the rest of the line move forward, and then adding the first `D` people at the back.

### How it Works: Full Walkthrough

1.  **Create a Temporary Array:** Create a new array, let's call it `tempArr`, of size `D`.
2.  **Copy First `D` Elements:** Copy the first `D` elements from `arr` into `tempArr`.
3.  **Shift Remaining Elements:** Shift the elements from index `D` to `N-1` of `arr` to the beginning of `arr` (i.e., to indices `0` to `N-D-1`).
4.  **Copy Back from Temp Array:** Copy the elements from `tempArr` back into `arr`, starting from index `N-D` to the end.

### Diagrams & Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`

**Initial:**
`arr: [ 1 | 2 | 3 | 4 | 5 ]`
`N = 5, D = 2`

**Step 1 & 2: Copy first D elements to `tempArr`**
`tempArr: [ 1 | 2 ]`
`arr:     [ 1 | 2 | 3 | 4 | 5 ]`

**Step 3: Shift remaining (N-D) elements to the front**
Elements `arr[2]` to `arr[4]` (i.e., `3, 4, 5`) move to `arr[0]` to `arr[2]`.
`arr:     [ 3 | 4 | 5 | _ | _ ]`

**Step 4: Copy `tempArr` back to the end**
Elements from `tempArr` (i.e., `1, 2`) move to `arr[3]` to `arr[4]`.
`arr:     [ 3 | 4 | 5 | 1 | 2 ]`

**Final Output:** `[3, 4, 5, 1, 2]`

### Code Implementation: Pure Java

```java
import java.util.Arrays;

public class ArrayRotationTempArray {

    /**
     * Rotates an array to the left by D positions using a temporary array.
     * Time Complexity: O(N)
     * Space Complexity: O(D) or O(N) in worst case (D=N)
     *
     * @param arr The array to be rotated.
     * @param d The number of positions to rotate.
     */
    public static void rotateLeftTempArray(int[] arr, int d) {
        int n = arr.length;

        // Handle edge cases: empty array, single element, or no rotation needed
        if (n == 0 || d == 0 || n == 1) {
            return;
        }

        // Normalize D
        d = d % n;
        if (d == 0) {
            return;
        }

        // Step 1 & 2: Create temp array and copy first 'd' elements
        int[] tempArr = new int[d];
        for (int i = 0; i < d; i++) {
            tempArr[i] = arr[i];
        }

        // Step 3: Shift remaining (N-D) elements to the front
        // Elements from index 'd' to 'n-1' move to '0' to 'n-d-1'
        for (int i = d; i < n; i++) {
            arr[i - d] = arr[i];
        }

        // Step 4: Copy elements from tempArr back to the end
        // Elements from tempArr[0] to tempArr[d-1] move to arr[n-d] to arr[n-1]
        for (int i = 0; i < d; i++) {
            arr[n - d + i] = tempArr[i];
        }
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        System.out.println("Original Array 1: " + Arrays.toString(arr1));
        rotateLeftTempArray(arr1, 2);
        System.out.println("Rotated Array 1 (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

        int[] arr2 = {10, 20, 30, 40, 50, 60};
        System.out.println("Original Array 2: " + Arrays.toString(arr2));
        rotateLeftTempArray(arr2, 3);
        System.out.println("Rotated Array 2 (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]

        int[] arr3 = {7};
        System.out.println("Original Array 3: " + Arrays.toString(arr3));
        rotateLeftTempArray(arr3, 5);
        System.out.println("Rotated Array 3 (D=5): " + Arrays.toString(arr3)); // Expected: [7]

        int[] arr4 = {};
        System.out.println("Original Array 4: " + Arrays.toString(arr4));
        rotateLeftTempArray(arr4, 10);
        System.out.println("Rotated Array 4 (D=10): " + Arrays.toString(arr4)); // Expected: []
    }
}
```

### Time and Space Complexity Analysis

  * **Time Complexity: O(N)**
      * Copying to `tempArr`: `D` operations.
      * Shifting remaining elements: `N-D` operations.
      * Copying back from `tempArr`: `D` operations.
      * Total: `D + (N-D) + D = N + D` operations. Since `D <= N`, this is `O(N)`.
      * *Example:* If `N=1000`, it's roughly `1000 + D` operations, which is much better than `1000 * D`.
  * **Space Complexity: O(D)**
      * We use a `tempArr` of size `D`. In the worst case, `D` can be `N` (e.g., `D = N-1`), so it's effectively `O(N)` space.

### Strengths and Weaknesses

  * **Strengths:**
      * **Much faster** than brute-force (linear time).
      * Relatively **easy to understand** after the brute-force.
  * **Weaknesses:**
      * Uses **extra space** proportional to `D` (or `N` in worst case). For very large arrays where memory is a constraint, this might not be optimal.

### Edge Cases & Handling

  * All edge cases (empty, single element, `D=0`, `D=N`, `D>N`) are handled correctly by the initial checks and `d = d % n;` normalization.

### Common Mistakes to Avoid

  * **Incorrect loop bounds/indices:** This is the most common mistake. Double-check the start and end indices for each of the three loops (copying to temp, shifting, copying from temp).
      * `arr[i - d] = arr[i]` for shifting.
      * `arr[n - d + i] = tempArr[i]` for copying back.
  * **Not normalizing `D`:** Same as brute-force, `d = d % n;` is crucial.

-----

## Approach 3: Optimal Method (Reversal Algorithm)

This is the most clever and efficient approach. It performs the rotation in-place (without extra space) and in linear time. It's often asked in interviews to check if you know the "trick."

### How it Works: Full Walkthrough

The reversal algorithm works in three steps:

1.  **Reverse the first `D` elements** of the array.
2.  **Reverse the remaining `N-D` elements** of the array.
3.  **Reverse the entire array.**

Let's see why this works.
Consider array `A` and `B` where `A` is the first `D` elements and `B` is the remaining `N-D` elements.
Original: `[ A | B ]`

1.  Reverse `A`: `[ A^R | B ]` (where `^R` denotes reversed)
2.  Reverse `B`: `[ A^R | B^R ]`
3.  Reverse the entire array: `[ (A^R B^R)^R ]` which simplifies to `[ B | A ]`.
    This is exactly what a left rotation does\!

### Diagrams & Dry Run: `arr = [1, 2, 3, 4, 5]`, `D = 2`

**Initial:**
`arr: [ 1 | 2 | 3 | 4 | 5 ]`
`A = [1, 2]`, `B = [3, 4, 5]`

**Step 1: Reverse first `D` elements (0 to D-1)**
Reverse `[1, 2]` to `[2, 1]`
`arr: [ 2 | 1 | 3 | 4 | 5 ]`

**Step 2: Reverse remaining `N-D` elements (D to N-1)**
Reverse `[3, 4, 5]` to `[5, 4, 3]`
`arr: [ 2 | 1 | 5 | 4 | 3 ]`

**Step 3: Reverse the entire array (0 to N-1)**
Reverse `[2, 1, 5, 4, 3]` to `[3, 4, 5, 1, 2]`
`arr: [ 3 | 4 | 5 | 1 | 2 ]`

**Final Output:** `[3, 4, 5, 1, 2]`

### Code Implementation: Pure Java

```java
import java.util.Arrays;

public class ArrayRotationOptimal {

    /**
     * Helper function to reverse a portion of an array.
     *
     * @param arr The array.
     * @param start The starting index (inclusive).
     * @param end The ending index (inclusive).
     */
    private static void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }

    /**
     * Rotates an array to the left by D positions using the reversal algorithm.
     * Time Complexity: O(N)
     * Space Complexity: O(1)
     *
     * @param arr The array to be rotated.
     * @param d The number of positions to rotate.
     */
    public static void rotateLeftOptimal(int[] arr, int d) {
        int n = arr.length;

        // Handle edge cases: empty array, single element, or no rotation needed
        if (n == 0 || d == 0 || n == 1) {
            return;
        }

        // Normalize D
        d = d % n;
        if (d == 0) {
            return;
        }

        // Step 1: Reverse the first 'd' elements (from index 0 to d-1)
        reverse(arr, 0, d - 1);
        // Example: [1,2,3,4,5], D=2 -> reverse(arr, 0, 1) -> [2,1,3,4,5]

        // Step 2: Reverse the remaining 'n-d' elements (from index d to n-1)
        reverse(arr, d, n - 1);
        // Example: [2,1,3,4,5] -> reverse(arr, 2, 4) -> [2,1,5,4,3]

        // Step 3: Reverse the entire array (from index 0 to n-1)
        reverse(arr, 0, n - 1);
        // Example: [2,1,5,4,3] -> reverse(arr, 0, 4) -> [3,4,5,1,2]
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5};
        System.out.println("Original Array 1: " + Arrays.toString(arr1));
        rotateLeftOptimal(arr1, 2);
        System.out.println("Rotated Array 1 (D=2): " + Arrays.toString(arr1)); // Expected: [3, 4, 5, 1, 2]

        int[] arr2 = {10, 20, 30, 40, 50, 60};
        System.out.println("Original Array 2: " + Arrays.toString(arr2));
        rotateLeftOptimal(arr2, 3);
        System.out.println("Rotated Array 2 (D=3): " + Arrays.toString(arr2)); // Expected: [40, 50, 60, 10, 20, 30]

        int[] arr3 = {7};
        System.out.println("Original Array 3: " + Arrays.toString(arr3));
        rotateLeftOptimal(arr3, 5);
        System.out.println("Rotated Array 3 (D=5): " + Arrays.toString(arr3)); // Expected: [7]

        int[] arr4 = {};
        System.out.println("Original Array 4: " + Arrays.toString(arr4));
        rotateLeftOptimal(arr4, 10);
        System.out.println("Rotated Array 4 (D=10): " + Arrays.toString(arr4)); // Expected: []
    }
}
```

### Time and Space Complexity Analysis

  * **Time Complexity: O(N)**
      * Each `reverse` call iterates through a portion of the array.
      * `reverse(0, d-1)`: `D` operations.
      * `reverse(d, n-1)`: `N-D` operations.
      * `reverse(0, n-1)`: `N` operations.
      * Total operations: `D + (N-D) + N = 2N` operations. This is `O(N)`.
  * **Space Complexity: O(1)**
      * We only use a few constant variables and perform operations in-place. No extra array is created proportional to `N` or `D`.

### Strengths and Weaknesses

  * **Strengths:**
      * **Optimal in both time (O(N)) and space (O(1)) complexity.** This is the best you can do.
      * Highly valued in competitive programming and interviews.
  * **Weaknesses:**
      * Can be a bit **tricky to remember** the three steps and correct ranges if you don't understand the underlying logic (`(A^R B^R)^R = BA`).

### Edge Cases & Handling

  * All edge cases (empty, single element, `D=0`, `D=N`, `D>N`) are handled correctly by the initial checks and `d = d % n;` normalization. The `reverse` function also gracefully handles `start >= end`.

### Common Mistakes to Avoid

  * **Incorrect ranges for `reverse` calls:** This is the most critical.
      * First part: `0` to `d-1`
      * Second part: `d` to `n-1`
      * Whole array: `0` to `n-1`
  * **Forgetting `d = d % n;`:** Essential for correctness and efficiency when `D` is large.

-----

## Left Rotation vs. Right Rotation Logic

The concepts for left rotation can be easily adapted for right rotation.

**Problem:** Rotate array `arr` to the **right** by `D` positions.

**Example:** `arr = [1, 2, 3, 4, 5]`, `D = 2`
**Expected Output:** `[4, 5, 1, 2, 3]`

**The Trick:** Rotating an array to the right by `D` positions is equivalent to rotating it to the **left** by `N - D` positions\!

**Example:** `[1, 2, 3, 4, 5]`, `N=5`, Right `D=2`
Equivalent to Left `D' = N - D = 5 - 2 = 3`

Let's try Left rotation by 3 on `[1,2,3,4,5]`:

1.  `[1,2,3,4,5]` -\> Left by 1 -\> `[2,3,4,5,1]`
2.  `[2,3,4,5,1]` -\> Left by 1 -\> `[3,4,5,1,2]`
3.  `[3,4,5,1,2]` -\> Left by 1 -\> `[4,5,1,2,3]` (Matches Right rotation by 2\!)

**So, to implement right rotation using the optimal reversal algorithm:**

1.  Calculate effective `D_right = D % N`.
2.  Calculate equivalent left rotation `D_left = N - D_right`.
3.  Apply `rotateLeftOptimal(arr, D_left)`.

**Alternatively, for Right Rotation using Reversal Algorithm directly:**

1.  Reverse the last `D` elements.
2.  Reverse the first `N-D` elements.
3.  Reverse the entire array.

*Dry Run for Right Rotation by 2: `[1,2,3,4,5]`*

1.  Reverse last `D=2` elements (`[4,5]`): `[1,2,3,5,4]`
2.  Reverse first `N-D=3` elements (`[1,2,3]`): `[3,2,1,5,4]`
3.  Reverse entire array: `[4,5,1,2,3]` (Correct\!)

-----

## Reusing This Logic: Interviews, CP, and Real-Life

  * **Interviews:**
      * Always start with the brute-force to show you understand the problem.
      * Then, move to the temp array for better time complexity.
      * Finally, present the optimal reversal algorithm for O(1) space. This shows a complete understanding and problem-solving progression.
      * Be ready to explain the `d = d % n;` normalization.
      * Explain the time/space complexities clearly.
  * **Competitive Programming (CP):**
      * Go straight for the **optimal (reversal) algorithm**. Time and space constraints are usually tight.
      * The `d = d % n;` normalization is critical for large `D` values.
  * **Real-Life Use Cases:**
      * **Circular Buffers:** When implementing a fixed-size queue where oldest elements are overwritten by new ones. A rotation can represent the "start" of the valid data.
      * **Image Processing:** Some image transformations might involve pixel array rotations.
      * **Data Encryption/Decryption:** Simple rotation-based ciphers.
      * **Scheduling Algorithms:** If tasks are in a circular queue and you need to move the "current" task to the end after completion.

-----

## Practice Drills (Visualize Them Clearly\!)

Try these on paper, tracing the array elements.

1.  **Simple Left Rotation:**

      * Input: `arr = [10, 20, 30, 40, 50]`, `D = 2`
      * Expected Output: `[30, 40, 50, 10, 20]`
      * *Visualize:* See `10, 20` go to the end.

2.  **Left Rotation with `D > N`:**

      * Input: `arr = [A, B, C, D, E, F]`, `D = 8`
      * Expected Output: `[C, D, E, F, A, B]` (because `8 % 6 = 2`, so it's a left rotation by 2)
      * *Visualize:* Imagine rotating by 1, then 2, then notice it's the same as rotating by 2.

3.  **Right Rotation (using Left Rotation logic):**

      * Input: `arr = [1, 2, 3, 4, 5, 6, 7]`, `D = 3` (Right Rotation)
      * Expected Output: `[5, 6, 7, 1, 2, 3, 4]`
      * *Visualize:* `N=7`, Right `D=3` is Left `D' = 7-3 = 4`. So, Left rotate `[1,2,3,4,5,6,7]` by `4`.

-----

## Summary Comparison Table

| Feature          | Brute-Force (Rotate 1 by 1) | Better (Temp Array) | Optimal (Reversal Algorithm) |
| :--------------- | :-------------------------- | :------------------ | :--------------------------- |
| **Time Complexity** | O(N \* D)                    | O(N)                | O(N)                         |
| **Space Complexity** | O(1)                        | O(D) (or O(N))      | O(1)                         |
| **In-place?** | Yes                         | No (uses temp array)| Yes                          |
| **Ease of Understanding** | Very Easy                   | Easy                | Moderate (conceptually tricky)|
| **Pros** | Simplest to code            | Good time complexity| Optimal in both time & space |
| **Cons** | Very slow for large inputs  | Uses extra memory   | Less intuitive initially     |
| **Interview/CP Use** | Rarely (only as starting point) | Common, good fallback | **Highly Preferred** |

-----

## Mindmap / Structure for Retention

```
ARRAY ROTATION (LEFT by D places)
├── Problem Definition
│   ├── What it is (shift first D to end)
│   └── Use Cases (circular buffer, scheduling)
│
├── Approaches
│   ├── 1. Brute-Force (Rotate one by one, D times)
│   │   ├── How it works (temp, shift, place at end)
│   │   ├── Complexity: O(N*D) Time, O(1) Space
│   │   ├── Pros: Simple
│   │   └── Cons: Inefficient
│   │
│   ├── 2. Better (Using Temporary Array)
│   │   ├── How it works (copy first D to temp, shift rest, copy temp back)
│   │   ├── Complexity: O(N) Time, O(D) Space
│   │   ├── Pros: Faster (Linear Time)
│   │   └── Cons: Uses extra space
│   │
│   └── 3. Optimal (Reversal Algorithm)
│       ├── How it works (Reverse A, Reverse B, Reverse All)
│       │   └── [A | B] -> [A^R | B] -> [A^R | B^R] -> [(A^R B^R)^R] = [B | A]
│       ├── Complexity: O(N) Time, O(1) Space
│       ├── Pros: Most efficient (Optimal)
│       └── Cons: Conceptually less intuitive initially
│
├── Common Considerations for All Approaches
│   ├── Edge Cases (N=0, D=0, N=1, D=N, D>N)
│   │   └── Handling: `d = d % n;` is crucial
│   └── Common Mistakes (off-by-one, incorrect loop bounds)
│
├── Left vs. Right Rotation
│   ├── Right D places = Left (N-D) places
│   └── Direct Right Reversal (Reverse last D, Reverse first N-D, Reverse All)
│
├── Real-Life Applications & Interview Strategy
│   ├── Circular buffers, game states, scheduling
│   ├── Interview Progression: Brute -> Temp -> Optimal
│   └── CP Strategy: Go straight for Optimal
│
└── Practice Drills
    └── Dry run with various D and N values.
```
