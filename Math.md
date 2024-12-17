# Mathematical Concepts in Data Structures and Algorithms (DSA): Digits and Formulas

Mathematics, particularly number theory, plays a significant role in solving algorithmic problems that involve digits, operations, and formulas. These concepts help in the optimization and analysis of algorithms in DSA.

## 1. **Digits of a Number**

### Extracting Digits
To extract the digits of a number, we can use the following methods:

- **Modulus Operation**: To get the last digit of a number, we use:
  \[
  \text{digit} = n \mod 10
  \]
  Where \( n \) is the number, and \( \mod \) is the modulus operator.

- **Division Operation**: To remove the last digit of a number, we use:
  \[
  n = \frac{n}{10}
  \]

### Example: Extracting digits of a number
For \( n = 12345 \):
- Last digit: \( 12345 \mod 10 = 5 \)
- Remove last digit: \( 12345 \div 10 = 1234 \)

## 2. **Sum of Digits**

To find the sum of digits of a number, we can repeatedly extract the last digit and add it to the sum. This can be done with a loop.

### Formula for Sum of Digits:
\[
\text{Sum of digits}(n) = (n \mod 10) + \text{Sum of digits}(n // 10)
\]
Where \( // \) represents integer division.

### Example:
For \( n = 12345 \), the sum of digits is:
\[
1 + 2 + 3 + 4 + 5 = 15
\]

## 3. **Digit Count**

The number of digits in a positive integer \( n \) can be found using logarithms.

### Formula for Number of Digits:
\[
\text{Number of digits}(n) = \lfloor \log_{10}(n) \rfloor + 1
\]
Where \( \lfloor x \rfloor \) is the floor function, which gives the greatest integer less than or equal to \( x \).

### Example:
For \( n = 12345 \):
\[
\lfloor \log_{10}(12345) \rfloor + 1 = 5
\]
So, the number 12345 has 5 digits.

## 4. **Power of 10**

In many algorithms, the power of 10 is used to shift digits or scale numbers. The power of 10 is represented as:
\[
10^k = 1 \underbrace{00\cdots0}_{k \text{ zeros}}
\]

For example:
- \( 10^2 = 100 \)
- \( 10^3 = 1000 \)

### Application: Multiplying by Powers of 10
To multiply a number by \( 10^k \), simply append \( k \) zeros to the number.

For \( n = 123 \) and \( k = 2 \):
\[
123 \times 10^2 = 12300
\]

## 5. **Factorial Formula**

Factorials are often used in combinatorial algorithms and recursion.

### Factorial Formula:
\[
n! = n \times (n-1) \times (n-2) \times \dots \times 1
\]
For example:
\[
5! = 5 \times 4 \times 3 \times 2 \times 1 = 120
\]

### Recursive Definition:
\[
n! = n \times (n-1)!
\]
Where \( 0! = 1 \) by definition.

## 6. **Combinatorics Formulas**

Combinatorics, a branch of mathematics, involves counting possible arrangements and selections. The most commonly used formulas are for permutations and combinations.

### Permutations Formula:
The number of permutations of \( n \) objects taken \( r \) at a time is:
\[
P(n, r) = \frac{n!}{(n-r)!}
\]

### Combinations Formula:
The number of combinations of \( n \) objects taken \( r \) at a time is:
\[
C(n, r) = \frac{n!}{r!(n-r)!}
\]

## 7. **Binomial Theorem**

The binomial theorem is used in problems involving the expansion of powers of binomials.

### Binomial Expansion:
\[
(a + b)^n = \sum_{k=0}^{n} C(n, k) \cdot a^{n-k} \cdot b^k
\]
Where \( C(n, k) \) is the combination formula, representing the number of ways to choose \( k \) items from \( n \).

### Example:
\[
(a + b)^2 = a^2 + 2ab + b^2
\]

## 8. **Modular Arithmetic**

Modular arithmetic is used in problems related to divisibility and remainders, which are common in hashing, cryptography, and number theory.

### Modular Addition:
\[
(a + b) \mod m = ((a \mod m) + (b \mod m)) \mod m
\]

### Modular Multiplication:
\[
(a \times b) \mod m = ((a \mod m) \times (b \mod m)) \mod m
\]

### Modular Inverse:
If \( a \) and \( m \) are coprime, the modular inverse of \( a \) modulo \( m \) is \( x \) such that:
\[
a \times x \equiv 1 \mod m
\]

### Example:
For \( a = 3 \) and \( m = 7 \), the modular inverse is 5, because:
\[
3 \times 5 \equiv 1 \mod 7
\]

## 9. **Digit Dynamic Programming**

In certain problems, dynamic programming is applied to digits to solve problems like counting the number of valid numbers or solving digit-based constraints.

### Example:
Counting the number of numbers from 1 to \( N \) that have no repeating digits can be solved using digit-based dynamic programming.

