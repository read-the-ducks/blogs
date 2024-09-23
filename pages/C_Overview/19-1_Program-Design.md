---
title: "Program Design in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_19-1_Program-Design
summary:
---

In this section, we will discuss some features of C and best practices to adopt when writing large programs.

### Modules
- Large programs in C can be seen as a set of independent **modules**. Each module is a collection of services offered to **clients** through an **interface** which describes its available services. The source code for the services are stored in the module's **implementation**. Dividing a program into modules allows us to achieve better reusability, maintainability, and better data abstraction.
- Modules allow us to only care about what they do/provide, while abstracting all details related to how operations are done. Abstraction makes it easier to work in a team, where each team member only needs to work with other member's code by interacting with each module's interface, with no need to dig deep in the code. There's also the notion of responsibility : each team member is responsible of a specific module in the code.
- Modules can be designed to be reusable in many programs. The interface they offer can be useful in many complex programs, which might lead us to reuse modules/avoid rewritting them.
- Separing our programs into several independent modules makes it easier to pinpoint the cause of a bug, and apply fixes to the 'faulty' module.

### Cohesion and Coupling
- Modules in our programs should not be random collections of declarations. They should offer High Cohesion and Low coupling.
- High Cohesion in the sense that all the elements in a specific module should be related to each other, or cooperating towards a common goal.
- Low Coupling in the sense that all modules should be independent from each other, as to ensure maintainability and reusability.

### Types of Modules
- There are four typical categories for modules in C : (1) A data pool, which is a collection of related variables and constants, (2) a library, which is a collection of related functions, (3) an abstract object, is a collection of function that operate on a hidden data structre, (4) an abstract data type, or ADT, is a type whose representation is hidden.

### Information Hiding
- Modules should aim to keep some information secret from its clients. Deliberately hiding information is known as **information hiding**, which offers security by not allowing clients to tamped with information, and flexibility to modify the module's functionning without touching its offered interfaces.
- The major tool for enforcing information hiding in C is the ```static``` storage class. As a remainder, the ```static``` storage class gives a variable a file scope and internal linkage, ths preventing from being accessed by other files. Functions can also be declared ```static``` to only be made accessible from other functions in the same file.

### Encapsulation
- Unlike other languages, there is almost no support for encapsulation in C. The only possible tool we can use for encapsulation are incomplete types, which can be described as "types that describe objects but lack information needed to determine their sizes". The best usage is to define a pointer type that references an incomplete type : ```typedef struct t *T;```, where the variable ```T``` is a pointer to a structure of tag ```t```. We can now declare variables of type ```T```, and pass them as argument to functions and perform other operations that are legal for pointers. Any attempts to access the data the pointer points to however will lead to unexpected behavior.
