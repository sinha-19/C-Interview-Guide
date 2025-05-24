# 8. Structures and Unions

---

## Introduction

Structures and unions are user-defined data types in C that allow grouping multiple data elements, possibly of different types, under a single name. They’re essential for modeling real-world entities, building complex data structures, and interfacing with hardware or protocols. Mastering their usage, memory layout, and differences is crucial for interviews and practical programming.

---

## Structures

### **A. What is a Structure?**

A structure (`struct`) groups variables (members) of different types together under one name.

**Syntax:**
```c
struct Student {
    char name[50];
    int age;
    float gpa;
};
```

**Declaration & Initialization:**
```c
struct Student s1 = {"Alice", 20, 3.8};
```

### **B. Memory Layout (Diagram)**

Suppose:
- `char name[50]` starts at 0x1000,
- `int age` at 0x1032,
- `float gpa` at 0x1036 (assuming no padding for simplicity).

```
Address   Size     Member         Example Value
0x1000    50 bytes name           "Alice" + padding
0x1032    4  bytes age            20
0x1036    4  bytes gpa            3.8
```

**Total size:** Sum of all members (plus possible padding for alignment).

### **C. Accessing Members**

```c
printf("%s is %d years old, GPA %.2f\n", s1.name, s1.age, s1.gpa);
```

### **D. Array of Structures**

```c
struct Student class[30];
class[0].age = 18;
```

### **E. Structures and Functions**

- Pass by value (copies structure):
    ```c
    void printStudent(struct Student s) { ... }
    ```
- Pass by reference (efficient, allows modification):
    ```c
    void updateGPA(struct Student *s, float newGPA) {
        s->gpa = newGPA;
    }
    updateGPA(&s1, 4.0);
    ```

### **F. Nested Structures**

```c
struct Date { int day, month, year; };
struct Student {
    char name[50];
    struct Date dob;
    float gpa;
};
```

---

## Unions

### **A. What is a Union?**

A union is like a structure, but all members share the **same** memory location. Only one member can be used at a time.

**Syntax:**
```c
union Data {
    int i;
    float f;
    char str[20];
};
```

**Declaration:**
```c
union Data d;
```

### **B. Memory Layout (Diagram)**

Suppose:
- `int i` (4 bytes)
- `float f` (4 bytes)
- `char str[20]` (20 bytes)

The size of the union is the size of its largest member (here, 20 bytes).

```
Address   Size     Holds
0x2000    20 bytes i, f, or str (overlapping)
```

### **C. Usage Example**

```c
d.i = 10;
printf("%d\n", d.i); // 10
d.f = 3.14;           // Overwrites i
printf("%f\n", d.f);  // 3.14
strcpy(d.str, "hi!"); // Overwrites previous data
printf("%s\n", d.str); // "hi!"
```

### **D. When to Use Unions**

- When you need a variable to hold one of several types, but only one at a time.
- Used in device drivers, protocol parsers, memory-efficient structures.

---

## Structures vs. Unions

| Feature    | Structure                                 | Union                                 |
|------------|-------------------------------------------|---------------------------------------|
| Memory     | Sum of all members (+ padding)            | Size of the largest member            |
| Access     | All members at once                       | Only one member at a time             |
| Use Case   | Records, complex data (e.g., Student)     | Efficient storage for mutually exclusive data |

---

## Bit-fields in Structures

Allow packing several bits into a single byte/word.

```c
struct Status {
    unsigned int isOn : 1;
    unsigned int error : 3;
    unsigned int code : 4;
};
```
- Useful for flags, hardware registers.

---

## Common Pitfalls

- **Union Overwrites:** Writing to one member destroys others’ values.
- **Padding/Alignment:** Structures may have gaps for alignment; use `sizeof` to check.
- **Returning Structures:** Large structures are expensive to return by value; prefer passing pointers.
- **Pointer Arithmetic:** Don’t treat structs/unions as arrays unless you really know their layout.

---

## Real-World Applications

- Modeling records: students, employees, products.
- Building linked lists, trees, and other data structures.
- Parsing network packets (often use unions for different interpretations).
- Hardware access with bit-fields and unions for control registers.

---

## Best Practices

- Prefer structs for related data; unions for memory savings when only one member is used at a time.
- Always initialize structure members.
- Use `typedef` to simplify structure usage:
    ```c
    typedef struct { int x, y; } Point;
    Point p1 = {1, 2};
    ```
- For portability, avoid assuming structure packing; use compiler directives if required.

---

## Interview Tips

- Draw diagrams showing structure and union memory layouts.
- Write code for common structure manipulations: sorting, searching.
- Discuss trade-offs between structures and unions.
- Explain bit-fields and their applications.

---

## Possible Follow-Up Questions

- How do you pass a structure to a function and modify its contents?
- What is the output if you store data in one union member and read from another?
- When do you use a union in embedded programming?
- How do bit-fields help in memory-constrained applications?
