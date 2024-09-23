---
title: "Arrays in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_8-1_Arrays
summary:
---

Arrays in C are an aggregate of variables of a certain type.

### One-Dimensional Arrays in C
- An array in C can be declared and initialized in the same line . If the initializer is shorter than the array, the rest of the elements are given the value of zero.
- The standard *C99* introduced designated initializers : ```int a[5] = {[1]=3, [3]=5};```
- We can use the ```sizeof``` operator to verify the size of an array : ```sizeof(a)/sizeof(a[0])```.

### Multidimensional Arrays in C
- Multidimensional Arrays can be declared and initialized in C using the following method : 


### Constant Arrays
- One-dimensional / Multidimensional array can be made constant in C. This means that they are not able to be modified in the code, and any attempt will be detected by the compiler.

### Variable-Length Arrays in C (C99 Standard)
- Variable-Length Arrays have been introduced in the standard *C99*. They cannot take an initializer value.
- Example in code :

```c
int n;
// We take n as an input from the user
int a[n];
```
