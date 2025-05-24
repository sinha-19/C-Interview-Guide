# 11. Preprocessor Directives

---

## Introduction

Preprocessor directives in C are instructions that are processed before the actual compilation of code begins. They start with a `#` and are handled by the preprocessor, which prepares the source code for the compiler. Understanding these directives is crucial for code modularity, portability, debugging, and conditional compilation.

---

## Types of Preprocessor Directives

### **A. File Inclusion**

- `#include`  
  Used to include the contents of another file, typically headers.

**Syntax:**
```c
#include <stdio.h>    // System header
#include "myheader.h" // User-defined header
```

**Difference:**  
- `<...>`: Searches standard system directories.
- `"..."`: Searches current directory first, then system directories.

---

### **B. Macro Substitution**

- `#define`  
  Defines symbolic constants or macros (textual substitution).

**Examples:**
```c
#define PI 3.14159
#define SQUARE(x) ((x) * (x))
```

- Simple constants: `PI` will be replaced with `3.14159` everywhere.
- Macros with parameters: `SQUARE(5)` becomes `((5) * (5)) → 25`.

**Best Practice:** Always parenthesize macro parameters to avoid precedence bugs.

---

### **C. Conditional Compilation**

- `#ifdef`, `#ifndef`, `#if`, `#else`, `#elif`, `#endif`
  Used to compile code conditionally, based on whether a macro is defined or a condition is true.

**Examples:**
```c
#define DEBUG

#ifdef DEBUG
    printf("Debug mode ON\n");
#endif

#ifndef RELEASE
    printf("Not Release build\n");
#endif

#if VERSION >= 2
    // Code for version 2 or higher
#else
    // Code for lower versions
#endif
```

- Useful for platform-specific code, debugging, or enabling/disabling features.

---

### **D. Macro Undefinition**

- `#undef`  
  Undefines a macro.

**Example:**
```c
#define TEMP 100
#undef TEMP
```

---

### **E. Other Useful Directives**

- `#pragma`: Compiler-specific instructions, e.g., suppressing warnings.
  ```c
  #pragma once // Ensures file is included only once (non-standard, but widely supported)
  ```

- `#error`: Produces a compilation error with a custom message.
  ```c
  #error "This code requires C99 or later."
  ```

- `#line`: Changes the current line number and file name for compiler messages (rarely used).
  ```c
  #line 100 "myfile.c"
  ```

---

## Preprocessor Flow (ASCII Diagram)

```
[Source Code] --(Preprocessor)--> [Expanded Source Code] --(Compiler)--> [Executable]
         |
     #include, #define, etc.
         v
[Textual replacement, file merging, conditional code removal]
```

---

## Real-World Applications

- Portability: Write cross-platform code by including/excluding OS-specific sections.
- Debugging: Enable/disable logging or assertions with `#ifdef DEBUG`.
- Code Optimization: Exclude expensive code for production builds.
- Header Guards: Prevent multiple inclusions of the same header file.

**Header Guard Example:**
```c
#ifndef MYHEADER_H
#define MYHEADER_H

// Contents of header

#endif
```

---

## Common Pitfalls

- Macro side-effects:  
  `#define DOUBLE(x) x + x` → `DOUBLE(3) * 3` becomes `3 + 3 * 3 = 12` (wrong!).  
  Use: `#define DOUBLE(x) ((x) + (x))`
- Forgetting parentheses in parameterized macros.
- Macros are not type-safe.
- Overusing macros instead of `inline` functions or enums.

---

## Best Practices

- Prefer `const`, `enum`, or `inline` over macros where possible for type safety.
- Always use header guards in user-defined headers.
- Use conditional compilation judiciously to avoid clutter.
- Clearly comment non-obvious macros.
- Avoid defining macros with very generic names (name clashes).

---

## Interview Tips

- Be ready to write and debug macro definitions.
- Explain the difference between macros and variables/functions.
- Discuss how conditional compilation enables cross-platform and debug/production builds.
- Show understanding of header guards and their necessity.

---

## Possible Follow-Up Questions

- What is the difference between `#include <file>` and `#include "file"`?
- How do macros differ from inline functions?
- How does conditional compilation help in debugging?
- What issues can arise from parameterized macros?
