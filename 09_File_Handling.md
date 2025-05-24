# 9. File Handling

---

## Introduction

File handling in C allows programs to store and retrieve data persistently from files on disk, making it possible to process large datasets, save state, and interact with the real world. Mastering file operations is essential for systems programming, data processing, and many real-life applications.

---

## File Pointers and File Structure

C uses a special type called `FILE *` to represent files. All file operations are performed through this pointer, which acts as a handle to the opened file.

**Declaration:**
```c
FILE *fp;
```

---

## Opening a File

Files are opened using `fopen()`, which requires a filename and a mode:

| Mode | Description                   |
|------|-------------------------------|
| "r"  | Read (must exist)             |
| "w"  | Write (creates/truncates)     |
| "a"  | Append (creates if not exist) |
| "rb"/"wb"/"ab" | Binary equivalents  |

**Example:**
```c
fp = fopen("data.txt", "r");
if (fp == NULL) {
    perror("Error opening file");
    return 1;
}
```
- Always check if `fp` is `NULL` (open failed).

---

## Reading and Writing

### **A. Character I/O**

- `fgetc(fp)` — Reads a single character.
- `fputc(c, fp)` — Writes a single character.

**Example:**
```c
char ch = fgetc(fp);
fputc('A', fp);
```

### **B. String and Line I/O**

- `fgets(buf, size, fp)` — Reads a line into `buf`.
- `fputs(str, fp)` — Writes a string.

**Example:**
```c
char buffer[100];
fgets(buffer, 100, fp);
fputs("Hello\n", fp);
```

### **C. Formatted I/O**

- `fprintf(fp, "format", ...)` — Like `printf` but to a file.
- `fscanf(fp, "format", ...)` — Like `scanf` but from a file.

**Example:**
```c
int x = 42;
fprintf(fp, "Value: %d\n", x);
fscanf(fp, "%d", &x);
```

### **D. Binary I/O**

- `fread(ptr, size, count, fp)` — Read `count` items of `size` bytes.
- `fwrite(ptr, size, count, fp)` — Write `count` items of `size` bytes.

**Example:**
```c
int arr[5] = {1,2,3,4,5};
fwrite(arr, sizeof(int), 5, fp);
fread(arr, sizeof(int), 5, fp);
```

---

## Closing a File

Always close files with `fclose(fp)` to flush buffers and release resources.

```c
fclose(fp);
```

---

## File Positioning

- `ftell(fp)` — Returns current file position.
- `fseek(fp, offset, whence)` — Set file position (`SEEK_SET`, `SEEK_CUR`, `SEEK_END`).
- `rewind(fp)` — Go back to the beginning.

**Example:**
```c
fseek(fp, 0, SEEK_END); // Move to end
long size = ftell(fp);  // Get file size
rewind(fp);             // Back to start
```

---

## Error Handling

- `feof(fp)` — Returns nonzero at end of file.
- `ferror(fp)` — Returns nonzero if a file error occurred.
- `perror("msg")` — Prints last error.

---

## Common Pitfalls

- Not checking if `fopen()` succeeded (NULL pointer).
- Forgetting to call `fclose()`, causing resource leaks.
- Buffer overruns with unsafe input (e.g., not bounding `fgets`).
- Reading/writing text as binary, or vice versa.
- Assuming file always exists or has expected data.

---

## Real-World Applications

- Logging and audit trails.
- Configuration files (read/write settings).
- Large data processing (databases, CSVs).
- Saving and restoring application state.

---

## Best Practices

- Always check return values from file functions.
- Use binary mode for non-text files to avoid corruption.
- Prefer `fgets` for reading lines safely.
- Handle errors gracefully, inform the user.
- Free any dynamically allocated buffers after use.

---

## Example: Copying a File Line by Line

```c
#include <stdio.h>
int main() {
    FILE *src = fopen("input.txt", "r");
    FILE *dest = fopen("output.txt", "w");
    if (!src || !dest) { perror("File error"); return 1; }
    char buffer[256];
    while (fgets(buffer, sizeof(buffer), src))
        fputs(buffer, dest);
    fclose(src);
    fclose(dest);
    return 0;
}
```

---

## Interview Tips

- Explain the differences between text and binary modes.
- Draw diagrams of file pointer movements and buffer usage.
- Be prepared to write code for reading, writing, or appending to files.
- Discuss error handling and resource management.

---

## Possible Follow-Up Questions

- What happens if you try to read from a file opened in write-only mode?
- How do you detect and handle end-of-file in a loop?
- How do you process a large file without loading it entirely into memory?
- What are the risks of not closing a file?
