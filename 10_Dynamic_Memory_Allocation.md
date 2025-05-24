# 10. Dynamic Memory Allocation

---

## Introduction

Dynamic memory allocation allows C programs to request and release memory at runtime, enabling flexible data structures like variable-length arrays, linked lists, trees, and more. Unlike static allocation, the size and lifetime of data can be determined while the program runs, making dynamic memory a cornerstone of systems and application programming.

---

## The Heap vs. The Stack

- **Stack:**  
  - Stores local variables and function call information.
  - Size fixed at compile time; limited in size.
  - Memory is released automatically when functions return.

- **Heap:**  
  - Used for dynamic memory allocation.
  - Managed by the programmer (via `malloc`, `free`, etc.).
  - Suitable for large or variable-sized data.

**ASCII Diagram:**  
```
|----------------|
|      Stack     |   <--- Grows downward
|----------------|
|      Heap      |   <--- Grows upward
|----------------|
|    Static/Code |
|----------------|
```

---

## Key Functions (from `<stdlib.h>`)

| Function                | Purpose                                               |
|-------------------------|------------------------------------------------------|
| `malloc(size_t size)`   | Allocates memory (uninitialized). Returns `void *`.  |
| `calloc(n, size)`       | Allocates zero-initialized memory for n elements.    |
| `realloc(ptr, newsize)` | Changes the size of previously allocated block.      |
| `free(ptr)`             | Releases previously allocated memory.                |

---

## Usage Examples

### **A. malloc**

```c
int *arr = (int *)malloc(5 * sizeof(int)); // Allocates memory for 5 ints
if (arr == NULL) {
    // Allocation failed
}
arr[0] = 42; // Use as normal array
free(arr);   // Release when done
```

### **B. calloc**

```c
float *data = (float *)calloc(10, sizeof(float)); // 10 floats, all zeroed
free(data);
```

### **C. realloc**

```c
arr = (int *)realloc(arr, 10 * sizeof(int)); // Resize for 10 ints
if (arr == NULL) { /* handle error */ }
```

- If `realloc` fails, original pointer remains valid, but you might lose it if not careful:
    ```c
    int *tmp = realloc(arr, newsize);
    if (tmp) arr = tmp;
    ```

### **D. free**

```c
free(arr); // Always free after use!
arr = NULL; // Good practice to avoid dangling pointer
```

---

## Memory Leaks & Dangling Pointers

- **Memory Leak:** Allocated memory is never freed. Over time, this exhausts available memory.
- **Dangling Pointer:** Pointer refers to memory that has already been freed.

**Example:**
```c
int *p = malloc(sizeof(int));
free(p);
*p = 10; // Dangling pointer: undefined behavior!
```

---

## Dynamic Arrays and Structures

**Array:**
```c
int n;
scanf("%d", &n);
int *arr = malloc(n * sizeof(int));
```
**Struct:**
```c
typedef struct { int x, y; } Point;
Point *p = malloc(sizeof(Point));
```

---

## Advanced: Linked Lists Example

Dynamic allocation enables building complex data structures:

```c
typedef struct Node {
    int data;
    struct Node *next;
} Node;

Node *head = malloc(sizeof(Node));
head->data = 1;
head->next = NULL;
```
- Each new node is dynamically allocated and linked.

---

## Common Pitfalls

- **Forgetting to free memory** (memory leaks).
- **Double freeing:** Calling `free` twice on the same pointer — leads to undefined behavior.
- **Dereferencing after free:** Leads to segmentation faults.
- **Not checking for NULL:** Always check if allocation succeeded.
- **Incorrect size:** Always use `sizeof(type)` for portability.

---

## Best Practices

- Initialize pointers to `NULL` after freeing.
- Always check the return value of allocation functions.
- Use `valgrind` or similar tools to detect leaks and misuse.
- Prefer `calloc` for zero-initialized memory.
- Avoid memory fragmentation by freeing as soon as no longer needed.

---

## Real-World Applications

- Large buffers (e.g., reading unknown-sized files).
- Dynamic data structures (lists, trees, graphs).
- Plug-in systems and dynamic libraries.

---

## Interview Tips

- Be ready to write code for dynamic array resizing, linked list insertion/deletion.
- Explain the difference between stack and heap allocation.
- Discuss error handling for failed allocations.
- Show awareness of memory leaks and how to avoid them.

---

## Possible Follow-Up Questions

- What is the difference between `malloc` and `calloc`?
- How can you check for memory leaks in your program?
- What happens if you free a pointer twice?
- How do you implement a dynamic 2D array in C?
