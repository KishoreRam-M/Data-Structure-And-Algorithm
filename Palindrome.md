# Palindrome Number

A **palindrome** is a number that reads the same forward as backward. For example, `121` is a palindrome, but `123` is not.

## Boundary Checks Before Looping

When checking if a number is a palindrome, we need to handle some special conditions before starting a loop to make the process faster.

### Important Conditions to Check First

1. **Negative Numbers**: A negative number can't be a palindrome because it has a negative sign at the beginning. So, if \( X < 0 \), we can return `false` right away.

2. **Numbers Ending in Zero**: If a number ends in zero (but is not zero itself), it can't be a palindrome. For example, `100` is not a palindrome. We check this condition using:
   \[
   \text{if } (X \% 10 == 0 \text{ and } X \neq 0)
   \]
   This ensures numbers like `100` or `1000` are not considered palindromes.

### Why Check Before the Loop?

Checking these conditions first means we can skip the loop entirely for numbers that are clearly not palindromes. This makes the algorithm faster.

### Examples:

1. **x = 100**:  
   - Since \( X \% 10 == 0 \) and \( X \neq 0 \), `100` is not a palindrome.

2. **x = 001**:  
   - Leading zeros don’t affect the value, so `001` is treated as `1`, which is a palindrome.

### Simple Code Example:
```java
public boolean isPalindrome(int x) {
    // Step 1: Check special cases
    if (x < 0 || (x % 10 == 0 && x != 0)) {
        return false;
    }
    
    // Step 2: Reverse half of the number and compare
    int reversed = 0;
    while (x > reversed) {
        reversed = reversed * 10 + x % 10;
        x /= 10;
    }
    
    // Step 3: Check if both halves are equal
    return x == reversed || x == reversed / 10;
}
