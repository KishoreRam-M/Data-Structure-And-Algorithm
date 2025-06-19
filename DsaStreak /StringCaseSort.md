## 🎯 **Problem Explanation: `caseSort()`**

Given a string `s` with a mix of **uppercase** and **lowercase letters**.

The goal is to:

  * **Sort uppercase letters separately.**
  * **Sort lowercase letters separately.**
  * **Crucially, preserve the *original case position* of each character.**

<!-- end list -->

```
┌─────────────────┐       ┌─────────────────┐
│ Input String: s │──────▶│ Mixed Case Chars│
└─────────────────┘       └─────────────────┘
        │
        ▼
┌──────────────────────────────────────┐
│  Original Cases  (fixed at position) │
└──────────────────────────────────────┘
        │
        ▼
┌──────────────────────────────────────┐
│  Character Value (changes, from sorted pool) │
└──────────────────────────────────────┘
```

-----

## 🧠 **How to Approach It (Step-by-Step Visuals)**

We break down the problem into distinct, visually explained phases.

### 🔹 **Phase 1: Separate Characters by Case**

Imagine two buckets: one for `UPPERCASE` and one for `lowercase`. We'll scan the input string character by character and put each into its respective bucket.

**Input String: `"dAeBc"`**

```
┌───────┐
│  'd'  │  (lowercase)
└───────┘
    │
    ▼
┌───────┐
│  'A'  │  (UPPERCASE)
└───────┘
    │
    ▼
┌───────┐
│  'e'  │  (lowercase)
└───────┘
    │
    ▼
┌───────┐
│  'B'  │  (UPPERCASE)
└───────┘
    │
    ▼
┌───────┐
│  'c'  │  (lowercase)
└───────┘
```

**Resulting Lists:**

```
          ┌─────────────┐               ┌─────────────┐
          │   upper     │               │    lower    │
          ├─────────────┤               ├─────────────┤
          │ ['A', 'B']  │               │ ['d', 'e', 'c'] │
          └─────────────┘               └─────────────┘
```

### 🔹 **Phase 2: Sort Character Lists Independently**

Now, we take each bucket and sort the characters within it alphabetically.

```
┌─────────────┐  Sort Alphabetically  ┌─────────────┐
│   upper     │ ────────────────────▶ │   upper     │
├─────────────┤                       ├─────────────┤
│ ['A', 'B']  │                       │ ['A', 'B']  │
└─────────────┘                       └─────────────┘

┌─────────────┐  Sort Alphabetically  ┌─────────────┐
│    lower    │ ────────────────────▶ │    lower    │
├─────────────┤                       ├─────────────┤
│ ['d', 'e', 'c'] │                       │ ['c', 'd', 'e'] │
└─────────────┘                       └─────────────┘
```

**Sorted Lists:**

```
          ┌─────────────┐               ┌─────────────┐
          │   upper     │               │    lower    │
          ├─────────────┤               ├─────────────┤
          │ ['A', 'B']  │               │ ['c', 'd', 'e'] │
          └─────────────┘               └─────────────┘
```

### 🔹 **Phase 3: Rebuild the String (Case Preservation)**

This is the core step. We'll iterate through the *original* string, checking the case at each position. Then, we pick the *next available sorted character* from the correct list (uppercase or lowercase) and append it to our new result string. We use `pointers` to keep track of our position in the sorted lists.

**Original String: `"dAeBc"`**
**Sorted `lower`: `['c', 'd', 'e']`**
**Sorted `upper`: `['A', 'B']`**

**Pointers:**
`lowerIndex = 0` (points to 'c')
`upperIndex = 0` (points to 'A')

**Iteration 1: `s[0] = 'd'`**

  * `'d'` is `lowercase`.
  * Take `lower[lowerIndex]` (`'c'`).
  * `result = "c"`
  * `lowerIndex` moves to 1.

<!-- end list -->

```
      Original:  d A e B c
                 ^
      Case:      Lowercase
      Sorted lower:  [c, d, e]
                     ^ (lowerIndex = 0)
      Result:    "c"
      New lowerIndex: 1
```

**Iteration 2: `s[1] = 'A'`**

  * `'A'` is `UPPERCASE`.
  * Take `upper[upperIndex]` (`'A'`).
  * `result = "cA"`
  * `upperIndex` moves to 1.

<!-- end list -->

```
      Original:  d A e B c
                   ^
      Case:      UPPERCASE
      Sorted upper:  [A, B]
                     ^ (upperIndex = 0)
      Result:    "cA"
      New upperIndex: 1
```

**Iteration 3: `s[2] = 'e'`**

  * `'e'` is `lowercase`.
  * Take `lower[lowerIndex]` (`'d'`).
  * `result = "cAd"`
  * `lowerIndex` moves to 2.

<!-- end list -->

```
      Original:  d A e B c
                     ^
      Case:      Lowercase
      Sorted lower:  [c, d, e]
                        ^ (lowerIndex = 1)
      Result:    "cAd"
      New lowerIndex: 2
```

**Iteration 4: `s[3] = 'B'`**

  * `'B'` is `UPPERCASE`.
  * Take `upper[upperIndex]` (`'B'`).
  * `result = "cAdB"`
  * `upperIndex` moves to 2.

<!-- end list -->

```
      Original:  d A e B c
                       ^
      Case:      UPPERCASE
      Sorted upper:  [A, B]
                          ^ (upperIndex = 1)
      Result:    "cAdB"
      New upperIndex: 2
```

**Iteration 5: `s[4] = 'c'`**

  * `'c'` is `lowercase`.
  * Take `lower[lowerIndex]` (`'e'`).
  * `result = "cAdBe"`
  * `lowerIndex` moves to 3.

<!-- end list -->

```
      Original:  d A e B c
                         ^
      Case:      Lowercase
      Sorted lower:  [c, d, e]
                            ^ (lowerIndex = 2)
      Result:    "cAdBe"
      New lowerIndex: 3
```

**✅ Final Output: `"cAdBe"`**

-----

## 👀 **Visual Explanation (Consolidated Flow)**

```
Input String: "d A e B c"
               │ │ │ │ │
               ▼ ▼ ▼ ▼ ▼
┌────────────────────────────────────┐
│ Step 1: Character Separation       │
└────────────────────────────────────┘
       ┌───────────┐      ┌───────────┐
       │   'd'     │      │   'A'     │
       │   'e'     │      │   'B'     │
       │   'c'     │      └───────────┘
       └───────────┘          upper
           lower (unsorted)
               │                  │
               ▼                  ▼
┌────────────────────────────────────┐
│ Step 2: Independent Sorting        │
└────────────────────────────────────┘
       ┌───────────┐      ┌───────────┐
       │   'c'     │      │   'A'     │
       │   'd'     │      │   'B'     │
       │   'e'     │      └───────────┘
       └───────────┘          upper (sorted)
           lower (sorted)
```

```
                      Sorted `lower`   [c] [d] [e]
                                      ^
                      Sorted `upper`   [A] [B]
                                      ^
┌────────────────────────────────────┐
│ Step 3: Reconstruct with Pointers  │
└────────────────────────────────────┘

Original String Position:
Index: 0  1  2  3  4
Char:  d  A  e  B  c

        Iterate through original string & check case:

        Pos 0 ('d' - lowercase)  ───▶ Get next from `lower` list (c)  ───▶ Result: "c"
        Pos 1 ('A' - uppercase)  ───▶ Get next from `upper` list (A)  ───▶ Result: "cA"
        Pos 2 ('e' - lowercase)  ───▶ Get next from `lower` list (d)  ───▶ Result: "cAd"
        Pos 3 ('B' - uppercase)  ───▶ Get next from `upper` list (B)  ───▶ Result: "cAdB"
        Pos 4 ('c' - lowercase)  ───▶ Get next from `lower` list (e)  ───▶ Result: "cAdBe"

                                                                  │
                                                                  ▼
                                                   Final Output: "cAdBe"
```

-----

## 🧩 **Concepts Involved (Diagrams)**

  * **String Traversal:**

    ```
    String S = "H e l l o"
                ^ ^ ^ ^ ^
                (Looping through each character by index)
    ```

  * **Character Classification (`Character.isUpperCase()`):**

    ```
    ┌──────────────────────────┐
    │     Character 'x'        │
    ├──────────────────────────┤
    │  isUpperCase('x')?       │
    │  isLowerCase('x')?       │
    └──────────────────────────┘
           │
           ▼
    ┌───────────┐   ┌───────────┐
    │ TRUE/FALSE│   │ TRUE/FALSE│
    └───────────┘   └───────────┘
    ```

  * **List Sorting (`Collections.sort()`):**

    ```
    Original List: [F, C, A, E, B, D]
                       │
                       ▼
    Collections.sort() (e.g., using Timsort in Java)
                       │
                       ▼
    Sorted List:   [A, B, C, D, E, F]
    ```

  * **Reconstruction of String (`StringBuilder`):**

    ```
    Initial: [ ] (Empty StringBuilder capacity)
             │
             ▼
    Append('c') ─▶ [c]
             │
             ▼
    Append('A') ─▶ [c, A]
             │
             ▼
    Append('d') ─▶ [c, A, d]
             │
             ▼
    ... (Efficiently building the string without creating new objects)
    ```

  * **Two-pointer Pattern:**

    ```
    List 1: [ A, B ]    <--- upperIndex
              ^
    List 2: [ c, d, e ] <--- lowerIndex
              ^

    (Pointers move independently based on case lookup in original string)
    ```

-----

## 📚 **Related Problems to Practice (Visual Cues)**

1.  **Sort a string while keeping digits in place**

    ```
    Input: "a1c2b"
           │ │ │ │ │
           ▼ ▼ ▼ ▼ ▼
    Output: "a1b2c" (letters sorted, digits fixed)
    ```

2.  **Replace vowels in order while preserving position**

    ```
    Input: "h_e_l_l_o" (Vowels: e, o)
           │ │ │ │ │
           ▼ ▼ ▼ ▼ ▼
    Sorted Vowels: e, o
    Output: "h_e_l_l_o" (if already sorted), or "h_o_l_l_e" (if vowels were 'o', 'e')
    ```

3.  **Reconstruct string using frequency map**

    ```
    Input: {a:2, b:1, c:3}
           │ │ │
           ▼ ▼ ▼
    Map: [a:2, b:1, c:3]
           │
           ▼
    Output: "aaabccc" (or "abcabca" based on specific reconstruction rules)
    ```

4.  **Merge two sorted strings by pattern**

    ```
    String 1: "ace"
    String 2: "bdf"
              │ │
              ▼ ▼
    Pattern: "S1 S2 S1 S2..."
              │ │
              ▼ ▼
    Output: "abcdef" (interleaved by pattern)
    ```

5.  **Arrange uppercase letters at even indexes**

    ```
    Input: "aBcDeF"
           │ │ │ │ │ │
           ▼ ▼ ▼ ▼ ▼ ▼
    Output: "FbcDeA" (or other patterns based on specific rules)
    ```

-----

## 💻 **Time and Space Complexity (Visuals)**

  * **Time Complexity**: `O(n log n)`

    ```
    Step 1 (Traversal):   O(N)   ┌───┐ ┌───┐ ┌───┐ ...
                                  │   │ │   │ │   │
    Step 2 (Sorting):    O(N log N) ┌───────────────┐
                                    │    SORTING    │
                                    └───────────────┘
    Step 3 (Reconstruction): O(N)   ┌───┐ ┌───┐ ┌───┐ ...
                                    │   │ │   │ │   │
    Overall Dominant Factor: Sorting
    ```

  * **Space Complexity**: `O(n)`

    ```
    Extra Lists:      [ Char List 1 ]  +  [ Char List 2 ]
                        (e.g., upper)      (e.g., lower)
    StringBuilder:    [ String Builder Internal Buffer ]
                        (to build the result)

    All scale with input size 'n'.
    ```

-----

## 🔁 **Variations of the Problem (Visual Handling)**

| Variation                  | How to Handle?                                | Visual Cue                                          |
| :------------------------- | :-------------------------------------------- | :-------------------------------------------------- |
| **Digits in string** | `Character.isDigit()` → Skip or put in 3rd list | `Input: "a1B2c"` \<br\> `Action: Ignore '1', '2' or put in separate list` |
| **Special characters** | `Character.isLetter()` → Keep as-is if not letter | `Input: "a!B@c"` \<br\> `Action: Keep '!', '@' fixed` |
| **Unicode characters** | `Character.isUpperCase()` handles them correctly | `Input: "ÄÖÜ"` \<br\> `Action: Works as expected`     |

-----

## 🚀 **How to Master This Topic (Roadmap Visuals)**

**📌 Roadmap:**

1.  **String Traversal & Reconstruction:**

    ```
    START ───▶ Read String ───▶ Process Char ───▶ Build Result ───▶ END
    ```

2.  **Filtering Characters by Property:**

    ```
    Char 'X' ───▶ isUpperCase() ? ─┐
                                    │─▶ Separate Lists
                  isDigit() ?   ───┘
    ```

3.  **Sorting Parts of a String:**

    ```
    Original String: [ P_1, P_2, Sorted_Part, P_3 ]
                                    ▲
                                    │
                                    (Only this section is sorted)
    ```

4.  **Two-pointer or Greedy Approaches:**

    ```
    ◀──── Left Pointer        Right Pointer ────▶
    [ Element 1, ..., Element N ]
    (Pointers move to satisfy conditions)
    ```

5.  **Case-Sensitive Sort Challenges:**

    ```
    Complex Sort Rule:
    IF Case_A THEN Sort_Rule_X
    ELSE IF Case_B THEN Sort_Rule_Y
    ```

**🧠 Tip**: Don’t just solve — **draw diagrams, explain your logic to someone, or write detailed comments like these\!**

-----

## 🧪 **Code with Comments (Integrated Flow)**

```java
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public static String caseSort(String s) {
        // --- Step 1: Initialize separate lists for cases ---
        // Bucket for uppercase characters
        ArrayList<Character> upper = new ArrayList<>();
        // Bucket for lowercase characters
        ArrayList<Character> lower = new ArrayList<>();

        // Iterate through the original string to populate lists
        // Original String: "dAeBc"
        // Loop Progress:
        //  s[0] = 'd' (lower) -> lower.add('d')
        //  s[1] = 'A' (upper) -> upper.add('A')
        //  s[2] = 'e' (lower) -> lower.add('e')
        //  s[3] = 'B' (upper) -> upper.add('B')
        //  s[4] = 'c' (lower) -> lower.add('c')
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (Character.isUpperCase(ch)) {
                upper.add(ch); // Add to uppercase bucket
            } else {
                lower.add(ch); // Add to lowercase bucket
            }
        }
        // Result after Step 1:
        // upper: ['A', 'B']
        // lower: ['d', 'e', 'c']


        // --- Step 2: Sort both lists independently ---
        // Sort uppercase characters alphabetically
        Collections.sort(upper);
        // Sort lowercase characters alphabetically
        Collections.sort(lower);
        // Result after Step 2:
        // upper: ['A', 'B']  <-- Now sorted
        // lower: ['c', 'd', 'e'] <-- Now sorted


        // --- Step 3: Reconstruct the string preserving case positions ---
        StringBuilder result = new StringBuilder(); // Efficiently build the new string
        int upperIndex = 0; // Pointer for sorted uppercase list
        int lowerIndex = 0; // Pointer for sorted lowercase list

        // Iterate through the original string again to decide which sorted char to pick
        // Original String: "dAeBc"
        // Loop Progress:
        //  s[0] = 'd' (lowercase) -> append lower.get(lowerIndex++) -> result="c"
        //      (lowerIndex becomes 1)
        //  s[1] = 'A' (uppercase) -> append upper.get(upperIndex++) -> result="cA"
        //      (upperIndex becomes 1)
        //  s[2] = 'e' (lowercase) -> append lower.get(lowerIndex++) -> result="cAd"
        //      (lowerIndex becomes 2)
        //  s[3] = 'B' (uppercase) -> append upper.get(upperIndex++) -> result="cAdB"
        //      (upperIndex becomes 2)
        //  s[4] = 'c' (lowercase) -> append lower.get(lowerIndex++) -> result="cAdBe"
        //      (lowerIndex becomes 3)
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (Character.isUpperCase(ch)) {
                result.append(upper.get(upperIndex++)); // Take next sorted uppercase
            } else {
                result.append(lower.get(lowerIndex++)); // Take next sorted lowercase
            }
        }

        return result.toString(); // Convert StringBuilder to final String
    }
}
```

-----

## 🔄 **Code + Summary (The Big Picture)**

```
             ┌──────────┐
             │  INPUT   │
             │ "dAeBc"  │
             └──────────┘
                  │
                  ▼
┌──────────────────────────────────────────────────────────┐
│   STEP 1: Separate Characters (by case)                  │
│                                                          │
│   ┌───────────────────┐    ┌───────────────────┐       │
│   │  Uppercase List   │    │  Lowercase List   │       │
│   │    ['A', 'B']     │    │   ['d', 'e', 'c'] │       │
│   └───────────────────┘    └───────────────────┘       │
└──────────────────────────────────────────────────────────┘
                  │
                  ▼
┌──────────────────────────────────────────────────────────┐
│   STEP 2: Sort Independently (each list)                 │
│                                                          │
│   ┌───────────────────┐    ┌───────────────────┐       │
│   │  Sorted Up. List  │    │  Sorted Low. List │       │
│   │    ['A', 'B']     │    │   ['c', 'd', 'e'] │       │
│   └───────────────────┘    └───────────────────┘       │
└──────────────────────────────────────────────────────────┘
                  │
                  ▼
┌──────────────────────────────────────────────────────────┐
│   STEP 3: Reconstruct String (using original case positions) │
│                                                          │
│   Original String: "d A e B c"                           │
│   Pointers:        ▲ ▲ ▲ ▲ ▲                             │
│   Result Builder:  [ ] [ ] [ ] [ ] [ ] (filled character by character) │
│                                                          │
└──────────────────────────────────────────────────────────┘
                  │
                  ▼
             ┌──────────┐
             │  OUTPUT  │
             │ "cAdBe"  │
             └──────────┘
```

This function elegantly solves the problem by breaking it into manageable sub-problems: **separation**, **sorting**, and **reconstruction**, all while meticulously preserving the original case structure. It's a classic example of using auxiliary data structures and a two-pointer approach for string manipulation.
