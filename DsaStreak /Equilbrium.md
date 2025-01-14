

### Example Array:
\[1, 2, 0, 3\]

### Step 1: Calculate the Total Sum of the Array
- Initialize `right` to 0.
- Iterate through the array and add each element to `right`.

**Initial Calculation**:
\[ \text{right} = 1 + 2 + 0 + 3 = 6 \]

### Step 2: Iterate Through the Array to Find the Equilibrium Point
- Initialize `left` to 0.
- For each element in the array, subtract the current element from `right` and compare `left` with `right`.



### Visual Representation:
```
Array:        [ 1, 2, 0, 3 ]
              |      ^
              |      |
Left Sum:    [ 1+2 ]   0
Right Sum:        0   [ 3+0 ]
Equilibrium at index 2
```

### Code Implementation:

```java
class Solution {
    // Function to find equilibrium point in the array.
    public static int findEquilibrium(int arr[]) {
        int left = 0;
        int right = 0;

        // Calculate the total sum of the array
        for (int i = 0; i < arr.length; i++) {
            right += arr[i];
        }

        // Iterate through the array to find the equilibrium point
        for (int i = 0; i < arr.length; i++) {
            right -= arr[i]; // Subtract the current element from the right sum

            if (left == right) {
                return i; // Return the 0-based index
            }

            left += arr[i]; // Add the current element to the left sum
        }

        // If no equilibrium point is found, return -1
        return -1;
    }
}
```
