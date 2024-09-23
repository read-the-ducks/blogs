---
title: "Strengths and Weaknesses of C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_1-2_Strengths-Weaknesses-of-C
summary:
---

### C Language Philosophy

The C programming language was mainly used to write operating systems and other systems software. It retains the following concepts as a core of its philosophy :

- *Low-Level* : C provides access to machine-level concepts (i.e. byte, addresses) to serve a suitable language for systems programming. It also provides access to the computer and operating system's built-in operations to make programs faster.

- *Small* : C provides less features than most languages. It also relies heavily on a library of standard functions.

- *Permissive* : C gives you a wider degree of control than other languages, and doesn't mandate error-checking like other languages.

### C Language Strengths

C has become widely popular due to the following strengths :

- *Efficiency* : C being intended as an alternative to Assembly, it is crucial that C programs run quickly while using the least amount of memory.

- *Portability* : C's association with UNIX and ANSI/ISO standards allowed to language to have an almost universal dialect across all PCs. Also, C compilers are widely available and easy to write on most machines.

- *Power* : C offers many data types and operators to perform complex operations in a few lines of codes.

- *Flexibility* : C's intended area of use was systems programming. However, it is not restricted to this area, and is used in applications of all kind (i.e. Embedded Systems, Data Processing...). C imposes very few restrictions and error-checking, allowing for more freedom when writing programs, at the cost of a more lengthy debug process.

- *Standard Library* : C's standard library contains a vast array of functions for I/O, string handling, storage allocation, and more complex operations.

- *Integration with UNIX* : C is used in a majority of UNIX applications. You must be probably familiar with Linux, a popular UNIX variant.

### C Language Weaknesses

As much as C offers strengths, its flexibility and closeness to the machine causes many issues to arise : 

- *Error-Prone* : As mentioned earlier, C is a very flexible language which does not enforce error-checking restrictions.

- *Difficult to Grasp* : C's flexibility allows programmers to use very specific low-level concepts or workarounds, making it very hard for any other programmer to pick-up and work with the code. 

- *Difficult to Modify* : C programs making use of flexible constructs (as mentioned above) are not necessarily designed with maintainability in mind. Also, C does not offer support for classes or packages, which usually allows to divide a program into more manageable pieces.

### Tips when using the C Language

To effectively take advantage of C's strengths, while mitigating its weaknesses, it is recommended to follow these suggestions :

- Avoid "tricks" and overly complex code 

- Stick to the C standard / Avoid using nonstandad features offered by compilers unless its absolutely necessary.

- Adopt a set of coding conventions (i.e. naming, indentation) 

- Use existing C libraries (including the standard library) rather than writing out your own functions.

- Use software tools, like debuggers and error-analysis tools (i.e. *lint*)

### Why should I use tools like Lint ?
- Lint checks C programs for potential errors not picked up by the compiler, like unused variables, unreachable code or nonportable code.

-  Most compilers can do a more thorough job of error-checking by specifying a 'warning level' (i.e. higher warning levels means more thorough checks).

- Apart from lint/debuggers, you can also use tools like 'bounds-checkers', which checks array subscripts/indices, and 'leak-finders', which helps locate memory leaks or dynamically allocated blocks of memory which are never deallocated.