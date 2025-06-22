# String Division Algorithm Explained

This document explains a Java solution for dividing a given string `s` into groups of a specified length `k`, filling the last group with a `fill` character if it's not full.

## Problem Description

Given a string `s`, an integer `k`, and a character `fill`, we need to divide `s` into substrings of length `k`. If the last substring is shorter than `k`, we append the `fill` character until its length becomes `k`.

## Solution Approach

The core idea is to iterate through the string and build groups of size `k`. We calculate the total number of groups required using ceiling division to account for any remaining characters. For each group, we append characters from the original string. If we run out of characters from the original string before a group is full, we append the `fill` character.

## Code Explanation

```java
class Solution {
    public String[] divideString(String s, int k, char fill) {
        int n = s.length(); // Get the length of the input string
        // Calculate the total number of groups needed.
        // (n + k - 1) / k is a common way to perform ceiling division (ceil(n/k)).
        int totalGroups = (n + k - 1) / k;
        
        // Initialize the result array of strings with the calculated total number of groups.
        String[] result = new String[totalGroups];
        
        // 'index' keeps track of our current position in the original string 's'.
        int index = 0; 
        
        // Iterate through each group that needs to be created.
        for (int i = 0; i < totalGroups; i++) {
            // Use a StringBuilder for efficient string manipulation within the loop.
            StringBuilder group = new StringBuilder();
            
            // For each group, append 'k' characters.
            for (int j = 0; j < k; j++) {
                // Check if we still have characters left in the original string 's'.
                if (index < n) {
                    // If yes, append the character from 's' and move to the next character.
                    group.append(s.charAt(index++));
                } else {
                    // If no, we've exhausted 's', so append the 'fill' character.
                    group.append(fill);
                }
            }
            // Convert the StringBuilder group to a String and store it in the result array.
            result[i] = group.toString();
        }
        // Return the array of divided strings.
        return result;
    }
}
```

### Step-by-Step Breakdown with Diagrams

Let's walk through the code with an example: `s = "abcdefg"`, `k = 3`, `fill = 'x'`

1.  **Initialization:**

      * `n = s.length()`: `n = 7`
      * `totalGroups = (n + k - 1) / k`: `(7 + 3 - 1) / 3 = 9 / 3 = 3`
      * `result = new String[3]`
      * `index = 0`

    <!-- end list -->

    ```
    s: "a b c d e f g"
    k: 3
    fill: 'x'

    n = 7
    totalGroups = 3
    result = [null, null, null]
    index = 0
    ```

2.  **First Group (i = 0):**

      * `group = new StringBuilder()`

    Inner loop (`j = 0` to `k-1`):

      * **j = 0:** `index < n` (0 \< 7) is true. `group.append(s.charAt(0))` -\> `group = "a"`, `index = 1`.
      * **j = 1:** `index < n` (1 \< 7) is true. `group.append(s.charAt(1))` -\> `group = "ab"`, `index = 2`.
      * **j = 2:** `index < n` (2 \< 7) is true. `group.append(s.charAt(2))` -\> `group = "abc"`, `index = 3`.

    After inner loop: `result[0] = group.toString()` -\> `result[0] = "abc"`

    ```
    s: "a b c d e f g"
            ^
            index = 3

    totalGroups = 3
    result = ["abc", null, null]
    group = "abc"
    ```

3.  **Second Group (i = 1):**

      * `group = new StringBuilder()`

    Inner loop (`j = 0` to `k-1`):

      * **j = 0:** `index < n` (3 \< 7) is true. `group.append(s.charAt(3))` -\> `group = "d"`, `index = 4`.
      * **j = 1:** `index < n` (4 \< 7) is true. `group.append(s.charAt(4))` -\> `group = "de"`, `index = 5`.
      * **j = 2:** `index < n` (5 \< 7) is true. `group.append(s.charAt(5))` -\> `group = "def"`, `index = 6`.

    After inner loop: `result[1] = group.toString()` -\> `result[1] = "def"`

    ```
    s: "a b c d e f g"
                    ^
                    index = 6

    totalGroups = 3
    result = ["abc", "def", null]
    group = "def"
    ```

4.  **Third Group (i = 2):**

      * `group = new StringBuilder()`

    Inner loop (`j = 0` to `k-1`):

      * **j = 0:** `index < n` (6 \< 7) is true. `group.append(s.charAt(6))` -\> `group = "g"`, `index = 7`.
      * **j = 1:** `index < n` (7 \< 7) is false. `group.append(fill)` -\> `group = "gx"`, `index` remains 7.
      * **j = 2:** `index < n` (7 \< 7) is false. `group.append(fill)` -\> `group = "gxx"`, `index` remains 7.

    After inner loop: `result[2] = group.toString()` -\> `result[2] = "gxx"`

    ```
    s: "a b c d e f g"
                      ^
                      index = 7

    totalGroups = 3
    result = ["abc", "def", "gxx"]
    group = "gxx"
    ```

5.  **Return `result`:**
    The loop finishes. The method returns `["abc", "def", "gxx"]`.

## Dry Run Example

Let's use a slightly different example for the dry run to illustrate the `fill` character's role more clearly:

**Input:**

  * `s = "hello"`
  * `k = 3`
  * `fill = '#'`

| Step | Variable `n` | Variable `totalGroups` | Variable `index` | Variable `i` | Variable `group` | Variable `j` | Condition `index < n` | Action | `result` array state |
| :--- | :----------- | :--------------------- | :--------------- | :----------- | :--------------- | :----------- | :-------------------- | :----- | :------------------- |
| 1    | 5            | `(5+3-1)/3 = 7/3 = 2`  | 0                | -            | -                | -            | -                     | Initialized variables | `[null, null]`       |
| 2    | 5            | 2                      | 0                | 0            | `new StringBuilder()` | -            | -                     | Start outer loop (i=0) | `[null, null]`       |
| 3    | 5            | 2                      | 0                | 0            | `""`             | 0            | `0 < 5` (True)        | `group.append('h')`, `index` becomes 1 | `[null, null]`       |
| 4    | 5            | 2                      | 1                | 0            | `"h"`            | 1            | `1 < 5` (True)        | `group.append('e')`, `index` becomes 2 | `[null, null]`       |
| 5    | 5            | 2                      | 2                | 0            | `"he"`           | 2            | `2 < 5` (True)        | `group.append('l')`, `index` becomes 3 | `[null, null]`       |
| 6    | 5            | 2                      | 3                | 0            | `"hel"`          | -            | -                     | Inner loop (j) ends | `[null, null]`       |
| 7    | 5            | 2                      | 3                | 0            | `"hel"`          | -            | -                     | `result[0] = "hel"`   | `["hel", null]`      |
| 8    | 5            | 2                      | 3                | 1            | `new StringBuilder()` | -            | -                     | Start outer loop (i=1) | `["hel", null]`      |
| 9    | 5            | 2                      | 3                | 1            | `""`             | 0            | `3 < 5` (True)        | `group.append('l')`, `index` becomes 4 | `["hel", null]`      |
| 10   | 5            | 2                      | 4                | 1            | `"l"`            | 1            | `4 < 5` (True)        | `group.append('o')`, `index` becomes 5 | `["hel", null]`      |
| 11   | 5            | 2                      | 5                | 1            | `"lo"`           | 2            | `5 < 5` (False)       | `group.append('#')`   | `["hel", null]`      |
| 12   | 5            | 2                      | 5                | 1            | `"lo#"`          | -            | -                     | Inner loop (j) ends | `["hel", null]`      |
| 13   | 5            | 2                      | 5                | 1            | `"lo#"`          | -            | -                     | `result[1] = "lo#"`   | `["hel", "lo#"]`     |
| 14   | 5            | 2                      | 5                | -            | -                | -            | -                     | Outer loop (i) ends | `["hel", "lo#"]`     |
| 15   | 5            | 2                      | 5                | -            | -                | -            | -                     | Return `result`       | `["hel", "lo#"]`     |

**Final Output:** `["hel", "lo#"]`

## Summary of Key Concepts

  * **Ceiling Division:** The formula `(n + k - 1) / k` is a common and efficient way to calculate `ceil(n/k)` for positive integers `n` and `k`. This ensures that even if `n` is not a perfect multiple of `k`, we allocate enough groups for all characters.
  * **StringBuilder:** Using `StringBuilder` for constructing the individual groups is more efficient than repeatedly concatenating `String` objects, especially in a loop. `String` concatenation creates new `String` objects, which can be performance-intensive.
  * **Index Tracking:** A single `index` variable is crucial for keeping track of the current position in the original string `s`, allowing us to sequentially pick characters for each group.
  * **Fill Character Logic:** The `if (index < n)` condition elegantly handles when to pick a character from `s` versus when to append the `fill` character, ensuring the last group is always of length `k`.

## Examples

Here are some more examples to solidify understanding:

**Example 1: Perfect Division**

  * `s = "abcdef"`, `k = 3`, `fill = 'x'`
  * `n = 6`, `totalGroups = (6 + 3 - 1) / 3 = 8 / 3 = 2`
  * **Output:** `["abc", "def"]`

**Example 2: Last Group Needs Filling**

  * `s = "abcde"`, `k = 3`, `fill = 'Z'`
  * `n = 5`, `totalGroups = (5 + 3 - 1) / 3 = 7 / 3 = 2`
  * **Output:** `["abc", "deZ"]`

**Example 3: String Shorter Than K**

  * `s = "hi"`, `k = 5`, `fill = '*'`
  * `n = 2`, `totalGroups = (2 + 5 - 1) / 5 = 6 / 5 = 1`
  * **Output:** `["hi***"]`

**Example 4: Empty String**

  * `s = ""`, `k = 3`, `fill = 'o'`
  * `n = 0`, `totalGroups = (0 + 3 - 1) / 3 = 2 / 3 = 0`
  * **Output:** `[]` (An empty array, as expected since there are no groups to form)

-----
