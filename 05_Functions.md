# 5. Functions

---

## Introduction

Functions are the building blocks of modular programming in C. They enable code reuse, abstraction, and clearer organization. Understanding functions deeply—how they’re defined, called, parameterized, scoped, and how memory is managed—is crucial for writing reliable and maintainable C code.

---

## Theoretical Foundations

### **A. What is a Function?**

A function is a named block of code that performs a specific task. Functions take input (parameters), process it, and (optionally) return a result. They help break large programs into manageable pieces, reducing redundancy and improving readability.

### **B. Function Components**

1. **Declaration (Prototype):**  
   Tells the compiler about a function’s name, return type, and parameters before it is used.
   ```c
   int add(int, int);
   ```

2. **Definition:**  
   Contains the actual code to be executed.
   ```c
   int add(int a, int b) {
       return a + b;
   }
   ```

3. **Call (Invocation):**  
   Executes the function with specified arguments.
   ```c
   int result = add(3, 5);
   ```

---

## Parameter Passing

### **A. Call by Value**

In C, arguments are passed by value by default. The function receives a **copy** of each argument.

```c
void increment(int n) {
    n = n + 1; // Only modifies local copy
}
int main() {
    int x = 5;
    increment(x);
    printf("%d\n", x); // Outputs 5, not 6!
}
```

### **B. Call by Reference (via Pointers)**

Passing addresses (pointers) allows the function to modify the caller’s variables.

```c
void increment(int *n) {
    (*n) = (*n) + 1;
}
int main() {
    int x = 5;
    increment(&x);
    printf("%d\n", x); // Outputs 6
}
```

---

## Return Values

- Functions can return any data type, including structs.
- Use `void` for functions that don’t return a value.

```c
int max(int a, int b) {
    return (a > b) ? a : b;
}
void printHello() {
    printf("Hello\n");
}
```

---

## Scope and Lifetime

- **Local Variables:** Declared inside a function, exist only during its execution (stack memory).
- **Global Variables:** Declared outside functions, are accessible throughout the program.
- **Static Variables:** Inside functions, retain value between calls.

```c
void counter() {
    static int count = 0;
    count++;
    printf("%d\n", count);
}
```
Calling `counter()` repeatedly prints 1, 2, 3...

---

## Recursion

A function can call itself, directly or indirectly.

**Example: Factorial Calculation**
```c
int factorial(int n) {
    if (n <= 1) return 1;
    else return n * factorial(n - 1);
}
```

**Discussion:**
- Each call creates a new stack frame.
- Recursion must reach a base case to prevent stack overflow.

---

## Advanced Features

### **A. Function Pointers**

Functions’ addresses can be stored in pointers, allowing dynamic call selection.

```c
int add(int a, int b) { return a + b; }
int (*funcPtr)(int, int) = add;
printf("%d\n", funcPtr(2, 3)); // Outputs 5
```

### **B. Variadic Functions**

Functions like `printf` accept a variable number of arguments.

```c
#include <stdarg.h>
void printNumbers(int count, ...) {
    va_list args;
    va_start(args, count);
    for (int i = 0; i < count; i++)
        printf("%d ", va_arg(args, int));
    va_end(args);
}
```

---

## Memory and Stack Diagram

When a function is called:
- Its parameters and local variables are pushed onto the stack.
- When it returns, its stack frame is popped.

```
|   ...          |
|   main() vars  |
|   add() vars   | <-- stack grows down
|   ...          |
```

---

## Common Pitfalls

- **Mismatched Declarations and Definitions:** Parameters or types differ.
- **Forgetting Return Statement:** May cause undefined behavior.
- **Stack Overflow:** Due to excessive recursion.
- **Uninitialized Locals:** Can lead to unpredictable results.
- **Returning Address of Local Variable:** Dangerous, as local memory is reclaimed after function exits.
    ```c
    int* foo() {
        int x = 5;
        return &x; // BAD: x ceases to exist after return
    }
    ```

---

## Best Practices

- Keep functions short and focused on a single task.
- Document parameters, return values, and side effects.
- Prefer passing by value for small structs, by pointer for large data.
- Avoid global variables unless necessary.
- Use `const` with pointer parameters if you won’t modify the data.

---

## Real-World Applications

- Math libraries (e.g., `sqrt`, `cos`)
- Sorting/searching algorithms
- Device driver routines (via function pointers for callbacks)
- Modularizing code in large systems

---

## Interview Tips

- Explain stack frame layout and memory implications.
- Be able to write and trace recursive functions.
- Understand how function pointers enable callback mechanisms.
- Discuss the trade-offs between recursion and iteration.

---

## Follow-Up Interview Questions

- What happens if you forget to return a value from a non-void function?
- How does the C compiler know which function to call (name mangling in C vs C++)?
- Can you write a function that returns a pointer to a function?
- How do static variables in functions behave across multiple calls?
