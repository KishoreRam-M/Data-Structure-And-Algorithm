# Armstrong Number

An **Armstrong Number** (also known as a **Narcissistic Number**) is a number that is equal to the sum of its own digits each raised to the power of the number of digits.

For example:
- `153` is an Armstrong number because:
  \[
  1^3 + 5^3 + 3^3 = 153
  \]
- `9474` is an Armstrong number because:
  \[
  9^4 + 4^4 + 7^4 + 4^4 = 9474
  \]

## Best Method to Find Armstrong Numbers

The best way to check if a number is an Armstrong number is to:
1. Extract each digit of the number.
2. Raise each digit to the power of the total number of digits.
3. Sum all the powered digits.
4. Compare the sum to the original number.

### Why This Method?

- **Time Complexity**: The time complexity of checking if a number is an Armstrong number is \( O(d) \), where \( d \) is the number of digits in the number. This is because we need to process each digit individually.
  
- **Space Complexity**: The space complexity is \( O(1) \), as we are only using a constant amount of space for variables (such as for the sum and the current digit).

### Steps to Check for Armstrong Number:

1. **Count the digits** in the number.
2. **Extract each digit** one by one.
3. **Raise each digit to the power of the number of digits**.
4. **Sum** the results of the powered digits.
5. If the sum is equal to the original number, it is an Armstrong number.

### Example:

Let's check if `153` is an Armstrong number:

1. The number of digits in `153` is 3.
2. Break the number into its digits: `1`, `5`, and `3`.
3. Raise each digit to the power of 3:
   \[
   1^3 = 1, \quad 5^3 = 125, \quad 3^3 = 27
   \]
4. Sum the results: 
   \[
   1 + 125 + 27 = 153
   \]
5. Since the sum is equal to the original number, `153` is an Armstrong number.

### Pseudocode for Armstrong Number Check:

```java
public boolean isArmstrong(int number) {
    int originalNumber = number;
    int sum = 0;
    int digits = String.valueOf(number).length(); // Find number of digits
    
    while (number != 0) {
        int digit = number % 10;
        sum += Math.pow(digit, digits); // Raise digit to the power of the number of digits
        number /= 10; // Remove the last digit
    }
    
    return sum == originalNumber; // Compare sum with the original number
}
