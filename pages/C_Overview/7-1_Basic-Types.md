---
title: "Basic Types in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_7-1_Basic-Types
summary:
---

### Integer Types in C
- Integers in C are signed by default, but we can specify them to be unsigned.
- The ```int``` type's length depends on the CPU we are using, but it is usually 32-bits. We can use ```short``` and ```long``` to as a prefix to the ```int``` type to denote that we want our integer value to be stored using more memory, therefore allowing it to have a higher absolute value.
- Table showing the number of bits used for different CPU types :

| Prefix | CPU Type | Number of bits allocated |
|-------- |  --------- | ------------------------- |
|```short```| 16-bits | 2-bits |
|```short```| 32-bits  | 2-bits |
|```short```| 64-bits | 2-bits |
| No prefix | 16-bits | 4-bits |
| No prefix | 32-bits | 4-bits |
| No prefix | 64-bits | 4-bits |
|```long```| 16-bits | 4-bits |
|```long```| 32-bits | 4-bits |
|```long```| 64-bits | 8-bits |

- We can determine the ranges of the integer types for a particular implementation by checking the ```<limits.h>``` header, which is part of the standard library.
- Overflow might occur if we perform operations on very large constants. The behavior for the operation might be 
- The standard *C99* has introduced support for a ```long long``` type
- If we'd like to use Octal constant, they must begin with a zero (e.g. ```017, 0377```).
- If we'd like to use Hexadecimal constant, they must begin with a ```0x``` (e.g. ```0x341, 0xFED```). Letters in a Hexadecimal constant can either be lower case or upper case.
- To force the compiler to treat an octal/hexadecimal constant as long, we can append ```L``` or ```l``` after it (e.g. ```0x341L, 0241l```). Same with long long constants by using ```LL``` or ```ll```.
- To force the compiler to treat an octal/hexadecimal constant as unsigned, we can append ```L``` or ```l``` after it (e.g. ```0x341U, 0241u```).

### Floating Types in C
- There are three different floating types in C : (1) ```float```, or single-precision floating-point, (2) ```double```, or double-precision floating-point, (3) ```long double```, or extended-precision floating-point. The precision offered by each type depends on how each computer stores floating point numbers. The IEEE standard is followed by most manufacturers.

### Character Types in C
- The ```char``` type vary from one computer to another, but mainly respect the ASCII code, which is a 7-bits code capable of representing 128 characters. ASCII is often extended to use 8-bits to support characters needed for non-english languages.
- C treats characters as integers, as they are encoded in binary. We can 'add' characters, which will addition their values according to the ASCII table, as well as other operations.
- Be warned : Depending on the compiler used, the ```char``` type can either be unsigned or signed by default.
- The functions ```getchar()``` and ```putchar(c)``` can be used to input/output characters. They are more efficient than ```scanf()``` and ```printf()``` when we only want to read characters, as these functions are designed to deal with more data types.

### Type Conversion in C
- The automatic conversion performed by the compiler when adding two different types are called **implicit conversions**, while the conversion performed manually by the programmer using the ```cast``` operator are called **explicit conversions**.
- The cast operator allows us to specify what type we'd like a value of a certain type to be cast to : ```i = (int) f```, with *f* being a character.

### Type Definition in C
- Type Definitions allow us to make a program more readable & portable. Here is an example : ```typedef int Money```. We can now use the type ```Money``` whenever we are dealing with monetary operations in our code, while knowing that it represents an integer type.
- There are two important differences between type definitions, and the macro definitions we saw previously. First, array and pointer types cannot be defined as macros. Second, ```typedef``` names are subject to the same scope rules as variables, whie macro names are only replaced by the preprocessor whenever they appear.

### The sizeof Operator
- The ```sizeof()``` operator allows us to determine how much memory is required to store values of a particular type (e.g. ```sizeof(int)```).