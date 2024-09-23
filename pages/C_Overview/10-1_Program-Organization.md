---
title: "Program Organization in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_10-1_Program-Organization
summary:
---

### Local Variables in C
- Variables declared in the body of a function are said to be local to the function.
- Static local variables causes them to have a *static storage duration*, which is a permanent storage location during the execution of the program. While a static variable in a function while not lose its value in-between executions, it will still remain inaccessible outside the scope of this function. Static variables might be interesting to use in many cases, including recursive function calls.
- Parameters to a function are also considered local variables.

### External Variables in C
- External variables are declared outside the body of any function, and can be used by any of them. They are referred to as *global variables*.
- External variables are convenient when many functions must share a variable, however it is sometimes better to use parameters due to some caveats : (1) We cannot modify external variables without affecting multiple functions, (2) If a wrong value is assigned to an external variable, then we need to go through all the functions calling it to identify the culprit, and (3) functions that rely on external variables are not self-contained, and cannot be easily ported to other programs.
- Make sure that you assign meaningful names to your external variables.

### Blocks in C
- The body of a function is a block. Like we've discussed previously, variables declared inside of a function block are considered as local variables.

### Scope in C
- If we have a variable with the same name across different functions, it doesn't mean that they all hold the same value or that assigning a value to that variable name will affect all other variables with the same name. It is a question of which scope the variable exists in (e.g. In main ? Inside of a function ?)

### Organizing a C program
- It is recommended to follow this organization for clarity in your C programs : (1) Preprocessing directives, (2) Type definitions, (3) Declaration of External Variables, (4) Function prototypes, (5) and Function Definitions.