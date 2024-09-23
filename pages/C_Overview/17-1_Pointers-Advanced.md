---
title: "Advanced Uses of Pointers in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_17-1_Pointers-Advanced
summary:
---

This section explores the use of pointers for dynamic storage allocation and pointing to functions

### Dynamic Storage Allocation
- The standand C Library has three memory allocation functions declared in the ```<stdlib.h>``` header : (1) ```malloc```, which allocated a memory block without initializing it, (2) ```calloc```, which allocates a block of memory and clears it, (3) ```realloc```, which resizes a previously allocated block of memory. ```malloc``` is the most used function out of the three. 
- These three functions return a 'generic' pointer of type ```void *``` to a memory address, as it doesn't know what type of variables we'd like to store memory for. The generic pointer will have its type converted to the pointer it is assigned to, without any cast necessary (although a cast can be applied).
- If these functions are not able to allocate the requested memory, they will return the **null pointer**. It is the programmer's responsibility to test if the returned pointer is null or not. The null pointer is represented by the macro ```NULL```, which we can use to test if a pointer is null. The ```NULL``` macro is present in most of the standard library headers.

### Dynamically Allocated Strings
- The ```malloc``` function has the following prototype : ```void *malloc(size_t size);```. When using ```malloc``` to store a string, remember to keep room for the null character. After initializing an array using this function, we can then use functions like ```strcpy()``` to initialize the block of memory. 

### Dynamically Allocated Arrays
- ```malloc``` can also be used for other types of arrays : ```int *a; a = malloc(n * sizeof(int));```. Make sure to allocate the proper amount of memory in your system by using the function ```sizeof(<type>)``` multiplied by the length of your array.
- ```calloc``` acts the same as ```malloc```, but sets all bits to zero, which is especially useful when allocating memory for structures. Its function prototype is ```void *calloc(size_t nmemb, size_t size);```.
- Example in code :

```c
int a*;
a = calloc(n, sizeof(int));

struct point {int x,y;} *p;
p = calloc(1, sizeof(struct point));
```

### Reallocating/Deallocating Storage

- ```realloc``` is used to resize a block in memory obtained from a previous ```malloc``` or ```calloc``` function call by either shrinking or expanding it. Its function prototype is ```void *realloc(void *ptr, size_t size);```. There are some rules to the function such as (1) when it expands a memory block, it doesn't initialize the bytes that were added to the block, (2) if it is called with a null pointer as an argument, it behaves like ```malloc```, (3) if it is called with zero as a second argument, it frees the memory block. Also, ```realloc```'s operation is not defined in the C standard, but it is expected to 'append' to an existing memory block if possible, and only move existing data if it is not possible to append additional blocks of free space to them. Make sure to update the pointer that ```realloc``` has returned, as it might have modified its existing location.
- Using these three functions must be done responsibly, as any allocated memory block we lose means of access to becomes unusable **garbage**, which might lead to **memory leaks**. In C, there is no garbage collection offered like other languages, and our program must free any used memory after it is complete.
- We can use the ```free``` function, defined in the ```<stdlib.h>``` library, to release block of memory pointed at by a pointer. Its function prototype is ```void free(void *ptr);```. Make sure to change what these pointers point to before reusing them, as using a 'freed/dangling' pointer might lead to unexpected behavior.

### Pointers to Pointers
- We can declare a pointer which points to anoher pointer : ```char **p; char *k; *p = k;```.

### Pointers to Functions
- We can pass pointers to function as arguments to other functions. Every function has a pointer by default, which is its own name without parentheses.
- Example in code :

```c
// Integrate has a function pointer as a parameter. It takes a double type as a parameter, and returns a double value.
double integrate(double (*f)(double), double a, double b);

// Inside of integrate, we call sin by doing (*f)(x)
result = integrate(sin, 0.0, PI/2);
```

### Restricted Pointers (standard C99)
- The standard *C99* introduced the keyword ```restrict``` which is mainly used with pointers. It is used to specify that an object is only accessible using a single pointer, and that therefore the compiler should not reload/check the object value for optimization purposes. If there is another pointer to the object different from the restricted pointer, and it modifies the object, it might lead to undefined behavior. The ```restrict``` keyword is mainly used during the fine-tuning process of a program.

### Flexible Array Members (standard C99)
- If a struct contains an array of characters, it must be initialized to a certain size. If we'd like to change the content of that array, we'd have to reallocate memory and change the length value of the character of arrays (usually stored in the struct as an int value). Usually, the struct is initialized first with a size of one, leading programmers to then allocate memory themselves and modify the length of the array. This is a popular 'struct hack' which was later acknowledged with the introduction of the ability to set the size of a character array to zero inside a struct, therefore becoming a 'flexible array'. This came with a few limitations however : The flexible array must appear last in the structure, the structure must have at least another member, copying the struct will take more steps to also transfer the elements inside the flexible array. Also, the flexible array will be considered an incomplete type.