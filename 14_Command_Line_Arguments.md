# 14. Command Line Arguments

---

## Introduction

Command line arguments allow users to pass information to a C program when it is executed from the terminal or command prompt. This enables flexible, scriptable, and interactive programs that can process files, options, and parameters without recompilation.

---

## Syntax

To accept command line arguments, the `main` function is defined as:

```c
int main(int argc, char *argv[])
```
or
```c
int main(int argc, char **argv)
```

- **`argc`** (Argument Count): Number of command line arguments (including the program name).
- **`argv`** (Argument Vector): Array of strings (character pointers) holding each argument.

---

## Example

Suppose you run:
```
./myprog file.txt 123 hello
```

- `argc == 4`
- `argv[0] == "./myprog"`
- `argv[1] == "file.txt"`
- `argv[2] == "123"`
- `argv[3] == "hello"`

**Sample Code:**
```c
#include <stdio.h>
int main(int argc, char *argv[]) {
    printf("Argument count: %d\n", argc);
    for (int i = 0; i < argc; i++)
        printf("Arg %d: %s\n", i, argv[i]);
    return 0;
}
```

---

## Converting Arguments

All command line arguments are strings. To use them as numbers, convert them with functions like `atoi`, `atof`, or `strtol`.

```c
#include <stdlib.h>
int n = atoi(argv[1]); // Converts first argument to integer
double d = atof(argv[2]);
```

---

## Practical Usage

- File processing (`myprog input.txt`)
- Setting options/flags (`myprog -v -o output.txt`)
- Batch processing or scripting

---

## Advanced: Parsing Options

You can manually parse options or use libraries like `getopt` (POSIX).

**Manual Example:**
```c
for (int i = 1; i < argc; i++) {
    if (strcmp(argv[i], "-h") == 0)
        printf("Help message\n");
    else if (strcmp(argv[i], "-v") == 0)
        printf("Verbose mode\n");
}
```

**With getopt:**
```c
#include <unistd.h>
int opt;
while ((opt = getopt(argc, argv, "hv")) != -1) {
    switch (opt) {
        case 'h': /* help */ break;
        case 'v': /* verbose */ break;
    }
}
```

---

## Common Pitfalls

- Not checking `argc` before using `argv[n]` (can cause out-of-bounds access).
- Forgetting that arguments are always strings.
- Not handling missing or malformed arguments.

---

## Best Practices

- Always check if required arguments are present.
- Print helpful usage messages if arguments are incorrect.
- Validate and sanitize inputs before using them.
- Document expected arguments for users.

---

## Interview Tips

- Be able to write code that takes and processes command line arguments.
- Show how to convert arguments to integers or floats.
- Explain how to handle optional arguments and flags.
- Discuss error checking and input validation.

---

## Possible Follow-Up Questions

- How do you handle a variable number of arguments?
- What happens if you try to access `argv[argc]`?
- How can you support options like `-h` or `--help`?
- How would you process arguments for a program that can take multiple input files?
