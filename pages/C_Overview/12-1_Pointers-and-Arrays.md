---
title: "Pointers and Arrays in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_12-1_Pointers-and-Arrays
summary:
---

Pointers can be used to point to array elements, which provides an alternative to using array subscripts to access array elements. Using pointers can sometime help achieve better efficiency, albeit with increased complexity.

### Pointer Arithmetic
- We can make a pointer ```p``` point to an element of an array ```a``` with the assignment ```p = &a[0];```. If we'd like our pointer to point at another element in the array, we can use **pointer arithmetic** to 'add'/'subtract' a value to the address it is pointing to. This way, if we have a pointer pointing to an address in an array of integers, we can assign to the pointer a summation/subtraction of its own address along with an integer that represents the amount of 'hops' we'd like to do in an array.
- The pointer already being initialized to a specific type, it will take this amount of 'hops' and multiply it by the size in bytes taken its target type, to be able to simulate hops in an array of a certain type.
- Subtracting two pointers to each other will give the distance between them, or the amount of 'hops' between them.
- We can also compare two pointers to elements using comparison operators, to find which one has the 'greatest address'. This might be affected by the computer architecture being little endian or big endian.
- In the standard *C99*, we can use pointers to point to elements created using compound literals. Example in code : ```int p* = (int []){3, 4, 6, 2};```

### Using Pointers for Array Processing
- Using pointer arithmetic can be an alternative to using array subscripting to iterate over arrays, although most compilers prove to be efficient enough to not warrant using pointer arithmetic at all.

### Using an Array Name as a Pointer
-  The name of an array can be used as a pointer to the first element in the array. Example in code : ```int a[10]; int p*; p = a;```.
- Arrays passed as argument to a function will always be passed as reference, considering that the array being passed is a pointer in itself.
- It's important to note that declaring an array of 10 integers will allocate space for 10 integers in memory, while declaring a pointer for an integer will simply allocate the memory required for the pointer variable itself.
- We can assign a pointer to point to an array, in which case we'd be able to use array subscripting to access elements in the array. Example in code : ```int i, a[10]; int p*; p = a; i = p[2]```.

### Pointers and Multidimensional Arrays
- Multidimensional arrays in C are stored in row-major form (i.e. row after row in memory). They are 'arrays of arrays', where each entry either stores another array or a finite entry. If we'd like to use a pointer to iterate over a 2-dimensional array to initialize it to zero row-by-row, we could do the following :

```c
int *p;
for (p = &a[0][0] ; p <= &a[NUM_ROWS-1][NUM_COLS-1]; p++)
{
    *p = 0;
}
```

- Alternatively, if we'd like to do the same column-by-column, we could apply the following method where ```p``` is a pointer to an array of *NUM_COLS* elements :

```c
// Column i will be initialized to zero in this code
int a[NUM_ROWS][NUM_COLS], (*p)[NUM_COLS], i;
for (p = &a[0] ; p <= &a[NUM_ROWS-1][NUM_COLS-1]; p++)
{
    (*p)[i] = 0;
}
```

- It is possible to use the name of a multidimensional array as a pointer. Be warned that it will point at *the first element* in the array, which might be another array in the case of a multidimensional array.

### Pointers and Variable-Length Arrays (C99 standard)
- In the standard *C99*, we can let pointers point to variable-length arrays that are both one dimensional and multidimensional.
- Example in code :

```c
int a[m][n], (*p)[n];
p = a; // First index of array a
```
