# 15. C Programming Best Practices & Interview Q&A

---

## C Programming Best Practices

### 1. **Write Clear, Readable Code**
- Use meaningful variable and function names.
- Indent code consistently.
- Add comments to explain complex logic or assumptions.

### 2. **Modularize Your Code**
- Break large programs into functions and modules.
- Use header files for declarations and implementation files for definitions.

### 3. **Use the Standard Library Wisely**
- Prefer standard functions (`strncpy`, `fgets`, `malloc`, etc.) over custom code for common tasks.
- Be aware of the limitations and pitfalls (e.g., buffer sizes).

### 4. **Practice Defensive Programming**
- Always check return values (e.g., `malloc`, `fopen`).
- Validate inputs and handle errors gracefully.
- Avoid "magic numbers"; use `#define` or `const`.

### 5. **Manage Memory Carefully**
- Free dynamically allocated memory with `free`.
- Initialize pointers to `NULL` and check before use.
- Avoid memory leaks and dangling pointers.

### 6. **Avoid Global Variables**
- Use local variables and pass data via function parameters.
- If globals are needed, encapsulate them in a module.

### 7. **Use `const` and `static` Appropriately**
- Use `const` for read-only data.
- Use `static` for persistent local variables or file-private globals.

### 8. **Prefer Enums over Macros for Constants**
- Enums are type-safe and scoped.

### 9. **Handle Files and Resources Properly**
- Always close files and release resources when done.

### 10. **Test, Debug, and Document**
- Use asserts (`assert.h`) for invariant checking.
- Write test cases for functions.
- Document usage, parameters, and return values.

---

## Frequently Asked Interview Questions (With Answers)

### Q1: **What is the difference between `malloc` and `calloc`?**
- `malloc(size)` allocates uninitialized memory.
- `calloc(n, size)` allocates zero-initialized memory for `n` elements of given size.

---

### Q2: **How do function pointers work in C?**
A function’s address can be stored in a pointer and called indirectly:
```c
int add(int x, int y) { return x + y; }
int (*fp)(int, int) = add;
int result = fp(2, 3); // result = 5
```

---

### Q3: **What is a segmentation fault?**
An error caused by accessing memory that the process doesn’t have rights to (e.g., dereferencing a NULL or dangling pointer, buffer overrun).

---

### Q4: **How do you prevent buffer overflows?**
- Always check bounds when copying or reading data.
- Use safe functions (`strncpy`, `fgets`).
- Validate input length before use.

---

### Q5: **What is the scope and lifetime of a static variable inside a function?**
Scope: Only inside the function.  
Lifetime: Entire execution of the program (retains value across calls).

---

### Q6: **How do you pass an array to a function?**
By passing the array name (which decays to a pointer):
```c
void foo(int arr[], int n) { ... }
```
You must also pass the size separately.

---

### Q7: **Why are header guards important?**
They prevent multiple inclusions of the same header file, which can cause redefinition errors.

---

### Q8: **How is a string represented in C?**
As an array of `char`, terminated by a null character (`'\0'`).

---

### Q9: **What is a memory leak?**
Memory that is allocated but not freed during program execution, leading to wasted resources.

---

### Q10: **How do you handle errors when opening files?**
Check if the returned file pointer is `NULL` and use `perror()` or `strerror(errno)` to print the error.

---

## Sample Coding Questions

1. **Reverse a string in place**
2. **Find the largest element in an array**
3. **Implement a linked list and basic operations**
4. **Write a function to check if a number is prime**
5. **Read/write a file line by line**

---

## Quick Reference: Common Mistakes

| Mistake                       | Solution                              |
|-------------------------------|---------------------------------------|
| Uninitialized pointers        | Always set to `NULL`                  |
| Buffer overflows              | Check sizes, use safe functions       |
| Not checking return values    | Always check for errors               |
| Memory leaks                  | Always call `free`                    |
| Shadowing global variables    | Use unique names, minimize globals    |
| Forgetting header guards      | Use `#ifndef ... #define ... #endif`  |

---

## Additional Resources

- [C Programming FAQ](https://c-faq.com/)
- [GeeksforGeeks C Programming](https://www.geeksforgeeks.org/c-programming-language/)
- [C Standard Library Reference](https://en.cppreference.com/w/c)

---

## Final Interview Tips

- Be clear and concise in explanations.
- Draw memory diagrams for pointer/structure questions.
- Test code for edge cases.
- Discuss trade-offs (efficiency, safety, readability).
- Show awareness of portability and standards compliance.
