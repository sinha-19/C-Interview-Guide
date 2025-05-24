# 6. Arrays and Strings

---

## Introduction

Arrays and strings are fundamental data structures in C. Understanding their memory layout, manipulation, and the subtle distinctions between arrays and pointers is key for both performance and correctness. In technical interviews, you’ll often face questions on array initialization, multidimensional arrays, pointer arithmetic, and safe string handling.

---

## Arrays in C

### **A. What is an Array?**

An array is a fixed-size, homogeneous collection of elements stored in contiguous memory locations. All elements must be of the same data type.

**Declaration & Initialization:**

```c
int numbers[5];                  // Declaration (uninitialized)
int primes[5] = {2, 3, 5, 7, 11}; // Declaration + Initialization
char vowels[] = {'a', 'e', 'i', 'o', 'u'}; // Size inferred
```

**Memory Layout (ASCII Diagram):**

Suppose `int arr[4] = {10, 20, 30, 40};` is stored at address 0x1000, on a system where `int` is 4 bytes:

```
Address   Value
0x1000    10   // arr[0]
0x1004    20   // arr[1]
0x1008    30   // arr[2]
0x100C    40   // arr[3]
```

- **Contiguous allocation** allows for efficient index-based access.

---

### **B. Multidimensional Arrays**

Used for matrices, grids, etc.

**Declaration:**
```c
int matrix[3][4];         // 3 rows, 4 columns
```

**Access:**
```c
matrix[1][2] = 7;
```

**Memory (Row-major order):**

```
matrix[0][0] matrix[0][1] ... matrix[2][3]
```
All elements are stored in a single contiguous block.

---

### **C. Array and Pointer Relationship**

- Array name acts as a pointer to the first element: `arr == &arr[0]`
- Can use pointer arithmetic: `*(arr + i) == arr[i]`

**Example:**
```c
int arr[3] = {1, 2, 3};
int *p = arr;
printf("%d", *(p + 2)); // Prints 3
```

**However:**  
- Array variables are not assignable: you cannot do `arr = p;`
- Arrays always have a fixed size after declaration.

---

### **D. Passing Arrays to Functions**

Arrays decay to pointers when passed to functions.

**Example:**
```c
void printArray(int a[], int size) {
    for (int i = 0; i < size; i++)
        printf("%d ", a[i]);
}
```

- The size must be passed separately.

---

### **E. Common Pitfalls**

- **Out-of-bounds Access:** Reading/writing beyond the declared size is undefined behavior.
- **Uninitialized Elements:** If not fully initialized, elements contain garbage values.
- **Array Size:** The size must be a constant at compile time (for static arrays).

---

## Strings in C

### **A. What is a String?**

A string in C is a sequence of characters terminated by the null character (`'\0'`).

**Declaration:**
```c
char name[10] = "Alice";    // 6 chars: 'A', 'l', 'i', 'c', 'e', '\0'
char word[] = {'H', 'i', '\0'}; // Also valid
```

**Memory Layout:**
```
Index   0    1    2    3    4    5
Value  'A'  'l'  'i'  'c'  'e' '\0'
```

### **B. String Input/Output**

**Using scanf and gets (unsafe):**
```c
char s[20];
scanf("%s", s);  // Stops at whitespace, no bounds checking
```
**Safer:**
```c
fgets(s, sizeof(s), stdin); // Reads line, prevents overflow
```

### **C. String Manipulation Functions**

From `<string.h>`:

- `strcpy(dest, src)`: Copy string
- `strncpy(dest, src, n)`: Copy n bytes
- `strlen(s)`: Length (not counting '\0')
- `strcmp(s1, s2)`: Lexicographic compare
- `strcat(dest, src)`: Concatenate
- `strchr(s, c)`: Find character

**Example:**
```c
char s1[20] = "Hello, ";
char s2[] = "World!";
strcat(s1, s2); // s1: "Hello, World!"
```

---

### **D. Manual String Manipulation**

**Reversing a string:**
```c
void reverse(char *str) {
    int n = strlen(str);
    for (int i = 0; i < n/2; i++) {
        char tmp = str[i];
        str[i] = str[n-1-i];
        str[n-1-i] = tmp;
    }
}
```

---

### **E. Pointers and Strings**

- Strings can be referenced by arrays or pointers:
```c
char arr[] = "test";
char *ptr = "test"; // String literal (read-only in modern C)
```
- Modifying string literals is undefined behavior.

---

## Real-World Applications

- **Strings:** User input, file paths, configuration, communication.
- **Arrays:** Buffers, tables, data processing, sensor data in embedded systems.

---

## Best Practices

- Always check array bounds before access.
- Use `fgets` or `scanf("%Ns", ...)` for safe string input.
- Prefer `strncpy`, `strncat`, and related functions for safer string manipulation.
- Remember that arrays decaying to pointers means size information is lost in functions.
- Consider dynamic allocation (`malloc`) for variable-length arrays.

---

## Common Pitfalls

- Buffer overflows from unchecked input or concatenation.
- Forgetting null terminator in manual string handling.
- Using uninitialized arrays or strings.
- Confusing arrays of characters (strings) with pointers to string literals.

---

## Interview Tips

- Be ready to write code for array reversal, searching, sorting, or simple string manipulations.
- Explain how C strings differ from those in higher-level languages (mutable, manual null-termination).
- Show understanding of how array and pointer arithmetic works.
- Discuss trade-offs between stack and heap arrays.

---

## Possible Follow-Up Questions

- How do you dynamically allocate an array of N elements?
- What is the difference between `char *str = "abc";` and `char str[] = "abc";`?
- How would you implement your own `strlen` or `strcpy`?
- How do multidimensional arrays work with pointer notation?
