---
title: "Strings in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_13-1_Strings
summary:
---

### Strings Literals
- **String literals** are a sequence of characters enclosed within double quotes (i.e. ```"Hello There!"```). C treats string literals as character arrays, which end with a null character *\0* (code 48 in ASCII).
- Example of String Literals in code : ```char *p = "abc";```.
- It is forbidden to modify string literals at they have an allocated space and are not part of an array.
- If our code contains two adjacent string literals, they will be automatically joined by the compiler : ```"ab" "c"``` will become ```"abc"```.

### String Variables
- String variables can be initialized & declared as follow : ```char date1[8] = "June 10th";```.
- Unlike String literals we can modify String variables.

### Using the C String Library
- The C library offers functions ```strcpy, strlen, strcat, strcmp``` to be able to perform string operations.

### Arrays of Strings
- We can use multidimensional arrays of characters to store multiple strings. A null character must be present at the end of each string.