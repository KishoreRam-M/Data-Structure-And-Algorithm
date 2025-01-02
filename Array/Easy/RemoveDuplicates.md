

---

### **Code Explanation**

#### **Method Signature**
```java
public int removeDuplicates(int[] arr)
```
This method takes an array `arr` of integers as input and removes duplicates in-place. It returns the length of the array after duplicates are removed.

---

#### **Key Variables**
1. **`j`**: 
   - Acts as a pointer to track the position of the last unique element.
   - Initially set to `0` (points to the first element of the array).

2. **`i`**:
   - Iterates through the array starting from index `1`.

---

#### **Loop Logic**
```java
for (int i = 1; i < arr.length; i++) {
    if (arr[i] != arr[j]) {
        arr[j + 1] = arr[i];
        j++;
    }
}
```
1. **`if (arr[i] != arr[j])`**:
   - Compares the current element `arr[i]` with the last unique element `arr[j]`.
   - If they are different, it means a new unique element is found.

2. **`arr[j + 1] = arr[i];`**:
   - Places the unique element at the position `j + 1` (next position for unique elements).

3. **`j++;`**:
   - Moves the pointer `j` forward to point to the newly added unique element.

---

#### **Return Value**
```java
return j + 1;
```
- The array is modified in-place, and `j + 1` represents the number of unique elements in the array.

---

### **Example Walkthrough**

#### Input:
```text
arr = [1, 1, 2, 3, 3, 4]
```

#### Execution Steps:

1. **Initialization**:
   - `j = 0` (points to the first element, `1`).

2. **Iteration**:
   - **Step 1**: `i = 1` → Compare `arr[1] (1)` with `arr[0] (1)` → No action (duplicate).
   - **Step 2**: `i = 2` → Compare `arr[2] (2)` with `arr[0] (1)` → New unique element:
     - `arr[1] = 2` → Update array to `[1, 2, 2, 3, 3, 4]`
     - `j = 1`
   - **Step 3**: `i = 3` → Compare `arr[3] (3)` with `arr[1] (2)` → New unique element:
     - `arr[2] = 3` → Update array to `[1, 2, 3, 3, 3, 4]`
     - `j = 2`
   - **Step 4**: `i = 4` → Compare `arr[4] (3)` with `arr[2] (3)` → No action (duplicate).
   - **Step 5**: `i = 5` → Compare `arr[5] (4)` with `arr[2] (3)` → New unique element:
     - `arr[3] = 4` → Update array to `[1, 2, 3, 4, 3, 4]`
     - `j = 3`

3. **Final State**:
   - `j = 3` → Unique elements are `[1, 2, 3, 4]`.

4. **Return**:
   ```java
   return j + 1; // 4
   ```

---

### **Output**
#### Input:
```text
[1, 1, 2, 3, 3, 4]
```
#### Output:
```text
4 // Length of unique elements
Modified Array: [1, 2, 3, 4]
```

---

1. **Time Complexity**: \(O(n)\)
   - Single traversal of the array.
2. **Space Complexity**: \(O(1)\)
   - No extra data structures are used.
3. **Algorithm**:
   - Uses two pointers to modify the array in-place, keeping track of unique elements.

T
