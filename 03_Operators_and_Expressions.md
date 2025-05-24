# 3. Operators and Expressions

---

## Introduction

Operators and expressions are the backbone of any computation in C. Mastering them is essential for writing efficient, readable, and bug-free code. In interviews, you’re often tested on subtle details, operator precedence, and common pitfalls. Here’s a deep dive into their theory, usage, and advanced considerations.

---

## Operator Categories

### **A. Arithmetic Operators**

Perform basic mathematical operations.

| Operator | Meaning          | Example         | Result        |
|----------|------------------|----------------|--------------|
| +        | Addition         | a + b          | Sum          |
| -        | Subtraction      | a - b          | Difference   |
| *        | Multiplication   | a * b          | Product      |
| /        | Division         | a / b          | Quotient     |
| %        | Modulus          | a % b          | Remainder    |

**Example:**
```c
int x = 10, y = 3;
printf("%d %d %d %d %d\n", x+y, x-y, x*y, x/y, x%y); // 13 7 30 3 1
```

---

### **B. Relational Operators**

Compare values and return 0 (false) or 1 (true).

| Operator | Meaning          |
|----------|------------------|
| ==       | Equal to         |
| !=       | Not equal to     |
| >, <     | Greater, Less    |
| >=, <=   | Greater/less-eq  |

**Example:**
```c
if (a != b) { printf("Not equal\n"); }
```

---

### **C. Logical Operators**

Used in conditions.

| Operator | Meaning      | Example            |
|----------|--------------|--------------------|
| &&       | Logical AND  | (a > 0 && b > 0)   |
| \|\|     | Logical OR   | (a == 0 \|\| b == 0) |
| !        | Logical NOT  | !(a > b)           |

---

### **D. Bitwise Operators**

Manipulate bits directly—key for embedded, low-level work.

| Operator | Meaning        | Example         | Result (for a=5,b=3) |
|----------|---------------|----------------|----------------------|
| &        | AND           | a & b          | 1                    |
| \|       | OR            | a \| b         | 7                    |
| ^        | XOR           | a ^ b          | 6                    |
| ~        | NOT           | ~a             | -6                   |
| <<       | Left shift    | a << 1         | 10                   |
| >>       | Right shift   | a >> 1         | 2                    |

**Example:**
```c
unsigned char a = 5; // 00000101
unsigned char b = 3; // 00000011
printf("%d\n", a & b); // 1
```

---

### **E. Assignment Operators**

| Operator | Meaning             | Example    |
|----------|---------------------|------------|
| =        | Assign              | a = b      |
| +=, -=   | Add/subtract assign | a += 5     |
| *=, /=   | Multiply/div assign | a *= 2     |

**Example:**
```c
int a = 10;
a += 5; // a = 15
```

---

### **F. Increment/Decrement**

| Operator | Meaning      | Example   |
|----------|-------------|-----------|
| ++       | Increment   | a++       |
| --       | Decrement   | --a       |

**Pre vs Post:**
```c
int a = 5, b;
b = ++a; // a=6, b=6
b = a++; // b=5, a=6
```

---

### **G. Conditional (Ternary) Operator**

Shorthand for if-else.
```c
int min = (a < b) ? a : b;
```

---

### **H. Comma Operator**

Evaluates expressions left to right, result is rightmost.
```c
int a = (b = 3, b + 2); // a=5
```

---

### **I. sizeof Operator**

Returns size in bytes.
```c
printf("%zu", sizeof(double)); // Typically 8
```

---

## Expressions

An **expression** is a combination of variables, constants, and operators that yields a value.

**Examples:**
- `a + b * c`
- `(x > y) && (z < 10)`

---

## Operator Precedence and Associativity

Operator precedence determines the grouping of terms; associativity determines the order of evaluation.

**Precedence Table (Partial):**

| Level | Operators                  | Associativity |
|-------|----------------------------|--------------|
| 1     | () [] -> .                 | Left to right|
| 2     | ++ -- (unary) + - ! ~ * &  | Right to left|
| 3     | * / %                      | Left to right|
| 4     | + -                        | Left to right|
| 5     | << >>                      | Left to right|
| ...   |                            |              |

**Example:**
```c
int result = 2 + 3 * 4; // result = 14, not 20
```

**Parentheses** override precedence:  
`int result = (2 + 3) * 4; // result = 20`

---

## Type Conversion

### **Implicit (Automatic) Conversion**

Occurs when operators have operands of different types.

**Example:**
```c
int i = 10;
float f = 5.5;
float result = i + f; // i promoted to float, result is float (15.5)
```

### **Explicit Conversion (Casting)**

Done manually by programmer.

**Example:**
```c
double pi = 3.14159;
int intPi = (int)pi; // intPi = 3
```

---

## Common Pitfalls

- **Assignment in Condition:**  
  ```c
  if (a = b) // Bug! assigns b to a, always true if b ≠ 0
  if (a == b) // Correct
  ```
- **Operator Precedence Confusion:**  
  ```c
  int x = 2, y = 3, z = 4;
  int res = x + y << z; // (x + y) << z = 5 << 4 = 80
  ```
- **Integer Division:**  
  ```c
  float f = 5 / 2; // 2, not 2.5! Both operands are int
  float f = 5.0 / 2; // 2.5
  ```
- **Pre- and Post-Increment Misuse:**  
  ```c
  int i = 5;
  printf("%d %d", i++, ++i); // Undefined behavior (never write like this)
  ```

---

## Real-World Applications

- Bitwise operators for device drivers, encryption, compression.
- Logical operators in complex control flows.
- Ternary for concise logic (e.g., absolute value: `int abs = (x < 0) ? -x : x;`).

---

## Best Practices

- Use parentheses to clarify precedence.
- Avoid complex expressions with multiple increments/decrements.
- Always use comparison (`==`) not assignment (`=`) in conditions.
- Consider type promotion in mixed-type arithmetic.

---

## Summary Table

| Operator Type    | Example      | Typical Use Case                      |
|------------------|-------------|---------------------------------------|
| Arithmetic       | a + b       | Calculations                          |
| Relational       | a == b      | Comparisons in control flow           |
| Logical          | a && b      | Compound conditions                   |
| Bitwise          | a & b       | Low-level hardware/data manipulation  |
| Assignment       | a += b      | Shorthand for updating variables      |
| Increment/Decrement | a++, --b | Loop counters                         |
| Conditional      | a ? b : c   | Inline conditional logic              |
| sizeof           | sizeof(x)   | Memory allocation, type introspection |

---

## Interview Tips

- Draw truth tables for logical and bitwise operators.
- Be ready for subtle bugs in expressions (side effects, precedence).
- Practice with bitwise hacks (swapping values, checking even/odd, etc.).

---

**Possible Follow-Up Interview Questions:**
- What is the output of `printf("%d", printf("Hi"));`?
- How does short-circuiting work for `&&` and `||`?
- Explain the difference between `&` (bitwise AND) and `&&` (logical AND).
- How can you swap two numbers without a temporary variable using operators?
