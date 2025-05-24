# 7. Pointers

---

## Introduction

Pointers are one of the most powerful and conceptually challenging features of C. They enable direct manipulation of memory, allow functions to modify variables outside their scope, support dynamic memory allocation, and are the backbone of data structures like linked lists and trees. Mastering pointers is essential for any serious C programmer.

---

## What is a Pointer?

A pointer is a variable that stores the **memory address** of another variable.  
Instead of holding data directly, it "points" to where the data lives in memory.

**Declaration:**
```c
int a = 10;
int *p;
p = &a; // p holds the address of a
```

- `*` in `int *p` means "pointer to int"
- `&a` gives the address of variable `a`

---

## Memory Representation (Diagram)

Suppose variable `a` is stored at address `0x1000`, and pointer `p` is stored at `0x2000`:

```
+----------+----------+----------+
| Address  |  Value   | Name     |
+----------+----------+----------+
| 0x1000   |   10     |   a      |
| 0x2000   | 0x1000   |   p      |
+----------+----------+----------+
```

- `a` stores 10
- `p` stores 0x1000, the address of `a`

**ASCII Diagram:**
```
[ a ] (0x1000) : 10
[ p ] (0x2000) : 0x1000 --> [ a ]
```

---

## Dereferencing

To access the value a pointer points to, use the dereference operator `*`:

```c
printf("%d\n", *p); // Prints 10, the value at address stored in p
```

---

## Pointer Arithmetic

Pointers can be incremented/decremented. When you add 1 to a pointer, it moves by the size of the type it points to.

```c
int arr[3] = {5, 10, 15};
int *ptr = arr; // points to arr[0]
ptr++;          // now points to arr[1]
printf("%d\n", *ptr); // 10
```

*If `int` is 4 bytes, ptr moves from 0x1000 to 0x1004.*

---

## Types of Pointers

- **NULL Pointer:** Points to nothing. Used for initialization and error checking.
  ```c
  int *p = NULL;
  if (p == NULL) { /* safe to check before dereferencing */ }
  ```
- **Wild Pointer:** Uninitialized pointer; points to an unknown location (dangerous).
  ```c
  int *p; // Wild! Always initialize.
  ```
- **Dangling Pointer:** Points to memory that has been freed or gone out of scope.
  ```c
  int *p = malloc(sizeof(int));
  free(p);
  // p is now dangling
  ```
- **Void Pointer:** Generic pointer (can point to any data type).
  ```c
  void *vp;
  int x = 5;
  vp = &x;
  printf("%d\n", *(int*)vp); // Must cast before dereferencing
  ```
- **Pointer to Pointer:** Stores address of another pointer.
  ```c
  int **pp;
  int *p = &x;
  pp = &p;
  ```

---

## Pointers and Functions

**Pass by Reference:**
```c
void update(int *p) { *p = 20; }
int a = 10;
update(&a); // a becomes 20
```

- Functions can modify variables in the caller by passing pointers.

**Returning Pointers:**
- Do **not** return pointers to local variables (memory is reclaimed).
- Safe to return pointers to static or dynamically allocated memory.

---

## Arrays and Pointers

- The name of an array acts as a constant pointer to its first element.
  ```c
  int arr[5];
  int *p = arr; // p = &arr[0];
  ```
- Pointer arithmetic allows traversal of arrays.

---

## Dynamic Memory Allocation

Pointers are essential for dynamic memory management.
```c
int *arr = (int *)malloc(5 * sizeof(int));
if (arr != NULL) {
    arr[0] = 10;
    free(arr); // Always free when done
}
```

---

## Common Pitfalls

- **Dereferencing NULL, wild, or dangling pointers** leads to segmentation faults.
- **Pointer arithmetic outside array bounds** is undefined behavior.
- **Memory leaks:** Allocated memory not freed, causing wasted resources.
- **Invalid casts:** Casting incompatible pointer types can corrupt data.

---

## Real-World Applications

- Building linked lists, trees, graphs.
- Dynamic arrays and buffers.
- Callback mechanisms (function pointers).
- Direct interaction with hardware (memory-mapped I/O).

---

## Best Practices

- Always initialize pointers, preferably to `NULL`.
- Free dynamically allocated memory.
- Check pointer values before dereferencing.
- Use `const` with pointers when not modifying the data.
- Avoid pointer arithmetic unless necessary and always stay within valid bounds.

---

## Advanced: Function Pointers

```c
int add(int a, int b) { return a + b; }
int (*funcPtr)(int, int) = add;
printf("%d\n", funcPtr(2, 3)); // 5
```
- Used for callbacks, implementing tables of functions, and more.

---

## Summary Table

| Feature                | Syntax/Example       | Notes                         |
|------------------------|---------------------|-------------------------------|
| Declare pointer        | int *p;             | Points to int                 |
| Address-of             | &x                  | Address of x                  |
| Dereference            | *p                  | Value p points to             |
| Pointer arithmetic     | p++, p--            | Moves by sizeof(type)         |
| NULL pointer           | int *p = NULL;      | Safe uninitialized value      |
| Dynamic allocation     | malloc/calloc/free  | Use with pointers             |
| Pointer to pointer     | int **pp;           | Multi-level indirection       |

---

## Interview Tips

- Draw diagrams to show pointer relationships.
- Demonstrate safe pointer usage and error checking.
- Be prepared to explain pointer/array equivalence and differences.
- Write code for linked lists, dynamic allocation, and pointer-based swapping.

---

## Possible Follow-Up Questions

- What happens if you dereference a NULL pointer?
- How do you implement a dynamic array in C?
- How are pointers used in linked lists?
- What is a function pointer and where is it used?
