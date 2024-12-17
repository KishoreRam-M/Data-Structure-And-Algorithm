# Basic Recursion

**Recursion** is a programming technique where a function calls itself in order to solve a problem. The recursive function keeps calling itself with smaller instances of the problem until it reaches a **base condition**, which stops further recursion.

### Key Concept:
- **Recursive Function**: A function that calls itself to solve smaller subproblems.
- **Base Condition**: The condition that terminates the recursion and prevents infinite function calls.

## Recursion Syntax

The basic structure of a recursive function consists of two main parts: the base condition and the recursive call.

```java
function fun() {
    // 1. Base Condition
    if (base_condition) {
        // Stop the recursion
        return;
    }

    // 2. Recursive Call
    fun();  // Function calls itself with a smaller input
    
    // 3. Function Operation
    // Perform necessary operations after recursive call (optional)
}
