---
title: "Pointers in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_11-1_Pointers
summary:
---

### Pointer Variables in C
- Main memory in most computers is divided into bytes with a unique address. We can declare **pointer variables** to point to specific addresses in memory or variables.

### Address and Indirection Operators
- Pointers in C can be declared using the following syntaxes : ```int *p; char *q;```. Pointers can point to other pointers.
- The Address operator ```&``` allow us to take the address of an existing variable. It is especially useful if we'd like to make a pointer point to an existing variable. Example in code : ```int i, p*; p = &i;```.
- The Indirection operator ```*``` can be used to access the data a pointer points to, or the data associated with a specific address in memory.

### Pointer Assignment
- As seen previously, we can make pointers point to exiting variables by using the Address operator, or we can simply set them equal to other pointers, using the assignment operator, for them to point to the same value as that pointer.

### Pointers as Arguments
- As mentioned previously, pointers can be used as function parameters to pass values by reference.
- We can use the ```const``` keyword to ensure that the value pointed at by a pointer is not modified in the function body.

### Pointers as Return Values
- We can use pointers as a return type, if we'd like to return a pointer to a specific object of a certain type.