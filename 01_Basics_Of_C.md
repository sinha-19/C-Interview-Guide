# 1. Basics of C

## Introduction and History

C is a general-purpose, procedural programming language created by Dennis Ritchie at Bell Labs in 1972. Its development was closely tied to the creation of the UNIX operating system, which was almost entirely written in C. Before C, systems were built in assembly, making C revolutionary for its time due to its combination of efficiency, portability, and expressive power.

## Key Features

- **Low-level Access:** C allows direct manipulation of hardware and memory through pointers, making it ideal for system-level programming.
- **Portability:** Programs written in C can be compiled and run on a wide range of hardware platforms with minimal changes.
- **Efficiency:** C code is compiled to efficient machine code, enabling high performance.
- **Modularity:** Code can be organized into functions and files, promoting reusability.
- **Rich Operator Set:** C provides arithmetic, logical, bitwise, and other operators for flexible programming.
- **Extensible:** Supports user-defined data types via structures and unions.

## Structure of a C Program

A typical C program is divided into several sections:

1. **Preprocessor Directives:** Start with `#`, like `#include <stdio.h>`, and are handled before compilation.  
2. **Global Declarations:** Variables or functions declared outside of `main()` are accessible throughout the program.
3. **The main Function:** Entry point of every C program.
4. **Function Definitions:** Code for custom functions, either before or after `main()`.

**Sample Program:**
```c
#include <stdio.h>      // Preprocessor directive

// Function prototype
void greet();

int main() {            // Entry point
    greet();            // Function call
    return 0;           // Exit status
}

void greet() {          // Function definition
    printf("Hello, World!\n");
}
```

## The Compilation Process

C source code undergoes several steps before it becomes a running program:

1. **Preprocessing:** Handles `#include`, `#define`, and conditional compilation.
2. **Compilation:** Converts source code to assembly code.
3. **Assembling:** Converts assembly to machine code (object files).
4. **Linking:** Combines object files and libraries into a single executable.

**ASCII Diagram:**
```
Source Code (.c)
      |
      v
Preprocessor
      |
      v
Compiler
      |
      v
Assembler
      |
      v
 Object Code (.o)
      |
      v
 Linker
      |
      v
 Executable
```

## Real-World Relevance

- **Operating Systems:** Most kernels (UNIX, Linux, Windows parts) are written in C.
- **Embedded Systems:** Device drivers, firmware, and microcontroller code widely use C.
- **Compilers and Interpreters:** Many are written in C for speed and direct hardware access.

## Common Pitfalls

- **Case Sensitivity:** `main` is not the same as `Main`.
- **Missing `main()` Function:** Every C program must have exactly one `main`.
- **Omitting Return Type:** Modern compilers require specifying the return type of `main` (preferably `int`).

## Best Practices

- Always use `int main(void)` or `int main(int argc, char *argv[])`.
- Comment your code for clarity.
- Use meaningful variable and function names.
- Modularize your code for better maintenance.

## Summary

C’s design strikes a balance between high-level programming convenience and low-level system access, making it foundational not just in academia but across industries. A solid understanding of C’s basics is crucial for any systems or embedded programmer, and its influence is deeply felt in modern languages like C++, Java, and even Python and Go.

---

**Possible Follow-Up Interview Questions:**
- Why is C known as a middle-level language?
- What makes C portable?
- How is C different from assembly and modern high-level languages?
- What are the limitations of C?
