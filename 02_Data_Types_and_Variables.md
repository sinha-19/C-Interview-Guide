# 2. Data Types and Variables

---

## Introduction

Data types and variables form the foundation of any C program. Understanding them deeply is crucial, as they dictate how your data is stored, manipulated, and interpreted in memory. Let’s break down the theory, practical code usage, memory implications, and best practices, ensuring you’re able to discuss and utilize them confidently in any interview scenario.

---

## Data Types in C

C offers a variety of data types, each with specific memory requirements and value ranges. These are grouped into:

### **A. Primary (Basic) Data Types**

| Type    | Typical Size | Range (32-bit)              | Example Usage        |
|---------|--------------|-----------------------------|---------------------|
| `char`  | 1 byte       | -128 to 127 / 0 to 255      | Letters, small ints |
| `int`   | 4 bytes      | -2,147,483,648 to 2,147,483,647 | Counting, loop indexes |
| `float` | 4 bytes      | 3.4E-38 to 3.4E+38          | Decimal numbers     |
| `double`| 8 bytes      | 1.7E-308 to 1.7E+308        | High-precision decimals |

> **Note:** Widths can differ between platforms. Use `sizeof(type)` to check.

### **B. Derived Data Types**
- **Arrays:** Collection of elements of the same type.
- **Pointers:** Variables storing memory addresses.
- **Structures:** Group different types under one name.
- **Unions:** Share memory among different types.

### **C. Enumeration (enum)**
- Named constants, e.g., `enum day {MON, TUE, WED};`

### **D. Void**
- Represents absence of type (e.g., `void foo();`, `void *ptr;`).

---

## Modifiers

C also allows type modifiers to adjust size and range:

- `short`/`long` (e.g., `short int`, `long double`)
- `signed`/`unsigned` (e.g., `unsigned int`)

**Example:**
```c
unsigned int u = 4000000000; // No negative numbers, larger positive range
```

---

## Variables: Declaration, Initialization, and Scope

### **A. Declaration and Initialization**

```c
int age;            // Declaration
age = 25;           // Assignment
float pi = 3.1415;  // Declaration + Initialization
char grade = 'A';   // Character variable
```

**Multiple variables:**
```c
int x = 1, y = 2, z = 3;
```

### **B. Memory Representation**

When you declare a variable, the compiler reserves a chunk of memory for it:

```
+----------+----------+----------+----------+
| 0x1000   | 0x1001   | 0x1002   | 0x1003   |
+----------+----------+----------+----------+
|     1    |     0    |     0    |     0    | // int x = 1;
+----------+----------+----------+----------+
   (Little Endian: least significant byte first)
```

### **C. Scope and Lifetime**

- **Local variables:** Declared inside functions/blocks. Created on stack, destroyed when scope ends.
- **Global variables:** Declared outside all functions. Exist for program lifetime.
- **Static variables:** Retain value between function calls but scope-limited.

**Example:**
```c
int globalVar = 10; // Global

void foo() {
    int localVar = 5;        // Local
    static int count = 0;    // Static local
    count++;
}
```

---

## Type Conversion

### **A. Implicit Conversion (Type Promotion)**
```c
int i = 10;
float f = i; // i promoted to float (10.0)
```
- Happens automatically; can lead to loss of precision or overflow in some cases.

### **B. Explicit Conversion (Type Casting)**
```c
float pi = 3.14;
int intPi = (int)pi; // intPi = 3 (fractional part lost)
```
- Use when you want to control conversion and avoid compiler warnings.

---

## Naming Rules and Best Practices

- Start with a letter or underscore, followed by letters, digits, or underscores.
- Case-sensitive (`Var` != `var`).
- Avoid reserved keywords (`int`, `float`, etc.).
- Use meaningful names (`totalMarks`, `averageScore`).

**Bad:**
```c
int x1, y2, z3;
```
**Good:**
```c
int studentAge, courseCount;
```

---

## Common Pitfalls

- **Uninitialized variables:** May contain garbage values—always initialize.
- **Overflow/underflow:** Assigning a value outside the variable's range causes wraparound or unpredictable results.
- **Signed/unsigned mismatch:** Can result in logic errors or infinite loops.
- **Shadowing:** Declaring a variable with the same name as an outer scope variable can lead to confusion.

---

## Real-World Relevance

- Variable types help conserve memory in embedded systems.
- Choosing the right type prevents bugs and increases code clarity.
- Understanding memory representation is crucial for debugging, especially with pointers and low-level programming.

---

## Sample Interview Discussion

> **Q:** How would you choose between `int`, `long`, and `unsigned int` for a variable that tracks the number of bytes read from a file?
>
> **A:** Since file sizes can be large and never negative, `unsigned long` is preferred for maximum positive range and clarity.

---

## Code Example: Overflow

```c
#include <stdio.h>
int main() {
    unsigned char c = 255;
    c = c + 1; // Overflows!
    printf("%u\n", c); // Outputs 0
    return 0;
}
```

---

## Summary Table

| Type             | Typical Size | Range                        | Use Case             |
|------------------|--------------|------------------------------|----------------------|
| `char`           | 1 byte       | -128 to 127 / 0 to 255       | Small ints, letters  |
| `int`            | 4 bytes      | -2B to +2B                   | General counting     |
| `unsigned int`   | 4 bytes      | 0 to 4B                      | Only positive values |
| `float`          | 4 bytes      | ~6 decimal digits            | Real numbers         |
| `double`         | 8 bytes      | ~15 decimal digits           | High-precision real  |

---

## Key Takeaways

- Data types control memory usage and correctness.
- Variable names and initialization are vital for maintainable, bug-free code.
- Always consider value range, signedness, and memory when choosing types.

---

**Possible Follow-Up Interview Questions:**
- How do data type sizes differ on 32 vs 64-bit machines?
- What happens if you assign a negative value to an unsigned variable?
- Explain type promotion in mixed-type arithmetic expressions.
