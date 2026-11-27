# ASSIGNMENT 5 – STORAGE CLASSES IN C

## Student Details
- **Student Name:RITHIKA SREE V
- **Register Number:1912260512
- **Subject:** C Programming
- **Assignment:** 5 – Storage Classes

## Compiler Details
- **Compiler:** GCC (GNU Compiler Collection)
- **Compiler Version:** Check using the command:

```bash
gcc --version
```

## Programs and Results

### Task 5.1 – Automatic Storage Class
**File:** `task5_automatic.c`

Demonstrates automatic local variables. The variable is initialized every time the function is called.

**Result:** Each function call returns 1001.

**Compilation and Execution:**
```bash
gcc task5_automatic.c -o automatic
./automatic
```

### Task 5.2 – Static Storage Class
**File:** `task5_static.c`

Demonstrates static local variables that retain their values between function calls.

**Result:** Generates sequential tokens 1001, 1002 and 1003.

```bash
gcc task5_static.c -o static
./static
```

### Task 5.3 – Global Storage Class Using extern
**Files:** `main.c` and `token.c`

Demonstrates global variables shared between multiple source files using the `extern` keyword.

**Result:** Generates sequential token numbers using a global counter.

```bash
gcc main.c token.c -o global
./global
```

### Task 5.4 – Register Storage Class
**File:** `task5_register.c`

Demonstrates the register storage class using a loop variable.

**Result:** Displays token numbers from 1001 to 1003.

```bash
gcc task5_register.c -o register
./register
```

### Task 5.5 – Two Independent Counters
**File:** `task5_two_counters.c`

Demonstrates two independent counters for vegetarian and non-vegetarian tokens.

**Result:** Both counters independently generate 1001, 1002 and 1003.

```bash
gcc task5_two_counters.c -o counters
./counters
```

## General Execution Instructions

1. Open the project folder in VS Code or a terminal.
2. Ensure GCC is installed.
3. Open the terminal in the project directory.
4. Compile the required C program using the GCC command.
5. Execute the generated program.
6. Verify the output.

## Conclusion

The assignment demonstrates the different storage classes in C: automatic, static, global and register. It also explains variable lifetime, scope, persistence and the use of global variables across multiple source files.
