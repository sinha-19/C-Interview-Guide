# 12. Storage Classes

---

## Introduction

Storage classes in C specify the scope (visibility), lifetime, and linkage of variables and functions. Understanding them is crucial for writing efficient, bug-free code, and for managing memory and name visibility across files and functions.

---

## The Four Storage Classes in C

### 1. **auto**

- **Default for local variables** (inside functions).
- **Scope:** Block in which it is defined.
- **Lifetime:** Created when the block is entered, destroyed on exit.
- **Linkage:** None (not accessible outside the block).
- **Explicit usage is rare** (e.g., `auto int x = 5;`).

**Example:**
```c
void foo() {
    auto int x = 10; // Same as just 'int x = 10;'
}
```

---

### 2. **register**

- Hints to the compiler to store the variable in a CPU register for **faster access** (optional).
- **Scope:** Block.
- **Lifetime:** Block.
- **Linkage:** None.
- **Cannot take the address** (`&`) of a register variable.

**Example:**
```c
void count() {
    register int i;
    for (i = 0; i < 1000; i++) { /* ... */ }
}
```

---

### 3. **static**

- **Local static:** Retains value between function calls.
- **Global static:** Limits scope to the file (internal linkage).
- **Scope:** Block (local) or file (global).
- **Lifetime:** Entire program (even if declared in a function).
- **Linkage:** None (for local), internal (for global).

**Local static Example:**
```c
void counter() {
    static int count = 0;
    count++;
    printf("%d\n", count);
}
// Each call prints an incrementing number
```

**Global static Example (file scope):**
```c
static int shared = 0; // Only accessible in this file
```

---

### 4. **extern**

- Declares a variable or function defined elsewhere (external linkage).
- Used to **share variables/functions across files**.
- **Scope:** Global.
- **Lifetime:** Entire program.
- **Linkage:** External.

**Example:**  
In `file1.c`:
```c
int shared = 5;
```
In `file2.c`:
```c
extern int shared;
void foo() { printf("%d\n", shared); }
```

---

## Scope, Lifetime, and Linkage Table

| Storage Class | Scope      | Lifetime      | Linkage      | Default Init | Keyword      |
|---------------|------------|---------------|--------------|--------------|-------------|
| auto          | Block      | Block         | None         | Garbage      | `auto`      |
| register      | Block      | Block         | None         | Garbage      | `register`  |
| static (local)| Block      | Program       | None         | Zero         | `static`    |
| static (global)| File      | Program       | Internal     | Zero         | `static`    |
| extern        | File/Global| Program       | External     | Zero         | `extern`    |

---

## Summary of Usage

- **auto:** Default for local variables, rarely written explicitly.
- **register:** For performance-critical loop counters (modern compilers usually ignore).
- **static:** For persistent local variables, private globals, and hiding functions/variables from other files.
- **extern:** For accessing global variables/functions across different files.

---

## Common Pitfalls

- Using `extern` without an actual definition elsewhere leads to linker errors.
- Taking address of a `register` variable is not allowed.
- Forgetting that `static` local variables retain their value between calls.
- Overusing global variables can make code hard to debug and maintain.

---

## Real-World Applications

- **static:** Implementing counters, caches, or hiding internal data in libraries.
- **extern:** Sharing configuration or state across multiple source files.
- **register:** Embedded/real-time systems (less relevant with modern compilers).

---

## Interview Tips

- Be able to explain scope, lifetime, and linkage clearly.
- Know when and why to use `static` and `extern`.
- Write examples showing differences between static local/global and extern variables.

---

## Possible Follow-Up Questions

- What is the default storage class for a local variable?
- Can you access a static variable from another file?
- What happens if you declare a global variable as `static`?
- Why can't you use `&` with a `register` variable?
