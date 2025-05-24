# 4. Control Structures (if, for, while, switch, etc.)

---

## Introduction

Control structures are the backbone of logic and decision-making in C programs. They dictate the flow of execution, allowing your code to branch, repeat, or choose between alternatives. Mastering these constructs enables you to write flexible, powerful, and efficient C programs.

---

## Types of Control Structures

### **A. Selection Statements**

#### 1. if, else if, else

**Syntax:**
```c
if (condition) {
    // Executes if condition is true
} else if (other_condition) {
    // Executes if other_condition is true
} else {
    // Executes if none of the above are true
}
```

**Example:**
```c
int score = 85;
if (score >= 90) {
    printf("Grade: A\n");
} else if (score >= 80) {
    printf("Grade: B\n");
} else {
    printf("Grade: C\n");
}
```

**Discussion:**
- The `if` statement evaluates the condition inside the parentheses.
- The `else if` and `else` allow multiple branches.
- Only the first true condition's block executes.

**Common Pitfalls:**
- Missing braces `{}` can lead to logic errors, especially with nested ifs.
- Assignment (`=`) instead of comparison (`==`).

---

#### 2. switch-case

**Syntax:**
```c
switch (expression) {
    case constant1:
        // statements
        break;
    case constant2:
        // statements
        break;
    default:
        // statements
}
```

**Example:**
```c
int day = 3;
switch (day) {
    case 1: printf("Monday\n"); break;
    case 2: printf("Tuesday\n"); break;
    case 3: printf("Wednesday\n"); break;
    default: printf("Other day\n");
}
```

**Discussion:**
- `switch` evaluates the expression and jumps to the matching `case`.
- `break` prevents "fall-through" into the next case.
- `default` is optional but handles unmatched cases.
- Only integer and enum types are allowed as switch expressions.

**Pitfalls:**
- Forgetting `break` causes fall-through, which can be intentional but is often a bug.
- Cases must use constant expressions.

---

### **B. Iteration (Looping) Statements**

#### 1. for Loop

**Syntax:**
```c
for (initialization; condition; increment) {
    // loop body
}
```

**Example:**
```c
for (int i = 0; i < 5; i++) {
    printf("%d ", i);
}
```

**Discussion:**
- Initialization runs once, condition checked before each iteration, increment runs after each iteration.
- Most useful when number of iterations is known in advance.

---

#### 2. while Loop

**Syntax:**
```c
while (condition) {
    // loop body
}
```

**Example:**
```c
int n = 5;
while (n > 0) {
    printf("%d ", n);
    n--;
}
```

**Discussion:**
- Condition checked before each iteration.
- Loop may not execute if condition is false initially.
- Good for input validation and indefinite repetition.

---

#### 3. do-while Loop

**Syntax:**
```c
do {
    // loop body
} while (condition);
```

**Example:**
```c
int i = 0;
do {
    printf("%d ", i);
    i++;
} while (i < 3);
```

**Discussion:**
- Loop body executes at least once, condition checked after execution.
- Useful for menu-driven programs.

---

### **C. Jump Statements**

#### 1. break

- Exits the nearest enclosing loop or switch.
- Used to stop iteration based on a condition.

#### 2. continue

- Skips the rest of the loop body and jumps to the next iteration.

**Example:**
```c
for (int i = 0; i < 5; i++) {
    if (i == 2) continue;
    printf("%d ", i); // Prints: 0 1 3 4
}
```

#### 3. return

- Exits from a function, optionally returning a value.

---

## Flow Diagrams

**if-else Example:**
```
[condition] --true--> [if block]
         |
         false
         |
     [else block]
```

**for Loop Example:**
```
[init] -> [condition] --false--> [exit]
               |
             true
               |
         [loop body]
               |
         [increment]
               |
           [condition] ...
```

---

## Advanced Usage and Best Practices

- **Nested Loops:** Used for multidimensional arrays, matrix operations.
    ```c
    for (int i = 0; i < rows; i++)
        for (int j = 0; j < cols; j++)
            // process arr[i][j];
    ```
- **Early Exit:** Use `break` to stop searching once found for efficiency.
- **Infinite Loops:** `while(1)` or `for(;;)` for event-driven or embedded systems, but always provide an exit condition.

---

## Common Pitfalls

- Modifying loop variables inside the loop can cause hard-to-find bugs.
- Off-by-one errors (e.g., `i <= n` vs `i < n`).
- Infinite loops due to incorrect conditions.
- In switch-case, not covering all possible values.

---

## Real-World Applications

- **Menu-driven programs:** `do-while` loops for repeated user input.
- **State machines:** `switch-case` for handling states/events.
- **Data processing:** `for` and `while` for iterating over arrays and files.

---

## Summary Table

| Structure     | Use Case                       | Syntax Example                |
|---------------|-------------------------------|-------------------------------|
| if-else       | Decision making                | `if (a > b) { ... }`          |
| switch-case   | Multi-way branching            | `switch(op) { case 1: ... }`  |
| for           | Counted loops                  | `for (i=0; i<n; i++)`         |
| while         | Conditional repetition         | `while (x > 0)`               |
| do-while      | At-least-once repetition       | `do { ... } while (cond);`    |
| break         | Early loop/switch exit         | `break;`                      |
| continue      | Skip to next loop iteration    | `continue;`                   |

---

## Interview Tips

- Be able to convert between for, while, and do-while loops.
- Practice dry-running complex nested loops and switch statements.
- Explain not just syntax, but why you choose a structure for a particular problem.

---

**Possible Follow-Up Interview Questions:**
- What's the difference between pre- and post-test loops?
- When would you use a switch-case over if-else?
- How do you break out of nested loops?
- What happens if you forget the break in a switch-case?
