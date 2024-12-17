# Greatest Common Divisor (GCD)

The **Greatest Common Divisor (GCD)** of two numbers is the largest number that divides both of them without leaving a remainder. For example, the GCD of `56` and `98` is `14`.

## Best Method to Find the GCD: Euclidean Algorithm

The **Euclidean Algorithm** is the most efficient way to compute the GCD of two numbers. It is based on the principle that the GCD of two numbers also divides their difference.

### Why Euclidean Algorithm?

- **Time Complexity**: The Euclidean algorithm has a time complexity of \( O(\log(\min(a, b))) \), where \( a \) and \( b \) are the two numbers for which the GCD is being calculated. This is due to the fact that the algorithm reduces the size of the numbers quickly.
  
- **Space Complexity**: The space complexity is \( O(1) \), since the algorithm only requires a constant amount of extra space for variables.

### Steps of the Euclidean Algorithm:

1. **Divide** the larger number by the smaller number.
2. **Take the remainder** of the division.
3. **Replace** the larger number with the smaller number and the smaller number with the remainder.
4. Repeat the process until the remainder becomes 0.
5. The GCD is the last non-zero remainder.

### Mathematical Representation:
Let \( a \) and \( b \) be two numbers:
- If \( b = 0 \), then \( \text{GCD}(a, b) = a \).
- Otherwise, \( \text{GCD}(a, b) = \text{GCD}(b, a \mod b) \).

### Example:
Let's find the GCD of \( 56 \) and \( 98 \):

1. \( 98 \mod 56 = 42 \)  
   (Divide 98 by 56, remainder is 42)
2. \( 56 \mod 42 = 14 \)  
   (Divide 56 by 42, remainder is 14)
3. \( 42 \mod 14 = 0 \)  
   (Divide 42 by 14, remainder is 0)

Since the remainder is 0, the GCD is \( 14 \).

### Pseudocode for Euclidean Algorithm:
```java
public int gcd(int a, int b) {
    while (b != 0) {
        int remainder = a % b;
        a = b;
        b = remainder;
    }
    return a;
}
