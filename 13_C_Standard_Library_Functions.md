# 13. C Standard Library Functions

---

## Introduction

The C Standard Library provides a rich set of built-in functions for common tasks such as input/output, memory management, string and character handling, math operations, and more. Mastery of these functions allows for efficient and portable code and is a frequent topic in technical interviews.

---

## Key Header Files and Their Functions

| Header         | Common Functions                                       |
|----------------|-------------------------------------------------------|
| `<stdio.h>`    | Input/output: `printf`, `scanf`, `fgets`, `fopen`    |
| `<stdlib.h>`   | General utilities: `malloc`, `free`, `atoi`, `rand`  |
| `<string.h>`   | String handling: `strcpy`, `strlen`, `strcmp`        |
| `<math.h>`     | Math ops: `sqrt`, `pow`, `sin`, `cos`                |
| `<ctype.h>`    | Character checks: `isalpha`, `isdigit`, `tolower`    |
| `<time.h>`     | Date/time: `time`, `clock`, `strftime`               |
| `<assert.h>`   | Assertions: `assert`                                 |

---

## Input/Output (`<stdio.h>`)

- **`printf`**: Formatted output.
- **`scanf`**: Formatted input.
- **`fgets`**: Read a line from a file or stdin.
- **`fputs`, `fgets`, `fgetc`, `fputc`**: File/string character/line IO.

**Example:**
```c
char buf[100];
printf("Enter name: ");
fgets(buf, 100, stdin);
printf("Hello, %s", buf);
```

---

## Memory Management (`<stdlib.h>`)

- **`malloc`, `calloc`, `realloc`, `free`**: Dynamic memory.
- **`exit`, `abort`**: Program termination.
- **`atoi`, `atof`, `strtol`**: String (ASCII) to number conversions.
- **`rand`, `srand`**: Pseudorandom numbers.

**Example:**
```c
int *arr = malloc(10 * sizeof(int));
if (!arr) exit(1);
free(arr);
```

---

## String Handling (`<string.h>`)

- **`strcpy`, `strncpy`**: Copy strings.
- **`strlen`**: Length of string.
- **`strcmp`, `strncmp`**: Compare strings.
- **`strcat`, `strncat`**: Concatenate strings.
- **`strchr`, `strstr`**: Search for char/substring.

**Example:**
```c
if (strcmp(s1, s2) == 0) printf("Equal\n");
```

---

## Mathematical Functions (`<math.h>`)

- **`sqrt`, `pow`, `sin`, `cos`, `fabs`, `log`**

**Example:**
```c
#include <math.h>
double r = sqrt(25.0); // 5.0
```

---

## Character Handling (`<ctype.h>`)

- **`isalpha`, `isdigit`, `isspace`, `tolower`, `toupper`**

**Example:**
```c
if (isdigit(c)) printf("Digit\n");
```

---

## Time and Date (`<time.h>`)

- **`time`, `clock`, `difftime`, `strftime`**

**Example:**
```c
#include <time.h>
time_t now = time(NULL);
printf("Seconds since Epoch: %ld\n", now);
```

---

## Assertions (`<assert.h>`)

- **`assert(expr)`**: Checks that `expr` is true; aborts if false (debugging).

**Example:**
```c
#include <assert.h>
assert(x > 0);
```

---

## Common Pitfalls

- Forgetting to include the appropriate header file.
- Buffer overflows (especially with string functions like `strcpy`).
- Not checking the return value of functions (e.g., `malloc`, `fgets`).
- Relying on non-portable functions or behavior.

---

## Best Practices

- Use safe function variants when available (e.g., `strncpy` over `strcpy`).
- Always check for errors (e.g., after `malloc`, `fopen`).
- Initialize buffers before use.
- Prefer standard functions over custom implementations for routine tasks.

---

## Real-World Applications

- Input validation and user interaction.
- Data parsing and manipulation.
- Randomized simulations.
- Time measurement and profiling.
- Asserting invariants in code (debugging).

---

## Interview Tips

- Be able to write and debug code using standard library functions.
- Know which header files are needed for common functions.
- Discuss the difference between standard and non-standard functions.
- Explain how to use functions safely (e.g., buffer sizes, return value checks).

---

## Possible Follow-Up Questions

- How do you safely copy a string in C?
- What does `strncpy` do if the source is shorter than the requested size?
- How do you generate a random number in a given range?
- How do you measure elapsed time in a C program?
- What happens if `assert` fails?
