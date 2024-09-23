---
title: "Structures, Unions, and Enumerations in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_16-1_Structures-Unions-Enumerations
summary:
---

- A Structure is a collection of values (members) of possibly different types. A Union is similar to a structure, although its members share the same storage, leading to only one value being valid at a time. An enumeration is an integer type whose values are named by the programmer.

### Structure Variables
- Example of a Structure Variable declaration :

```c
struct myStruct {
    int number;
    char name;
};
```
- In the standard *C99*, structures can directly be initialized in the code using **Designated Initializers**. Example in the code : ```{.number = 20, .name = "Joe"}```.
- A structure can be "duplicated" by using the assignment operator on another structure of the same type.

### Structure Types
- Example of a declaration of Structure tag :

```c
struct myStruct {
    int number;
    char name;
};

void f()
{
    struct myStruct obj1;
}
```
- We can also use ```typedef``` to define a genuine type name.
- Example of a declaration of Structure type using ```typedef``` (Note that the type name must come at the end of the ```typedef``` declaration):

```c
typedef struct  {
    int number;
    char name;
} myStruct;

void f()
{
    myStruct obj1;
}
```

- Like other variable types, structures can also be used as function parameters and return types. Passing structures as function parameters will cause copying of existing structures and might use a large chunk of memory, so it is better to pass structures by reference rather than value when possible.

### Nested Arrays and Structures
- It is possible to nest arrays and structures inside of other structures.
- It is also possible to create arrays of structures.

### Unions
- Union, like a structure, consists of more than one member. However, the compiler only allocates enough space for the largest of the memebers, and only has one member allocated at one time. If a new member is initialized, the old one will be overwritten.
- Union are mainly used inside of structures to save memory.
- We can create a genuine type name using unions with the ```typedef``` keyword. 

- Example of a declaration of Structure tag :

```c
union myUnion {
    int number;
    char name;
};
```

- Example of a declaration of Structure type using ```typedef``` (Note that the type name must come at the end of the ```typedef``` declaration):

```c
typedef union  {
    int number;
    char name;
} myUnion;
```

### Enumerations
- We can declare enumerations to have more expressive placeholders for integers in our code. Like both structures and unions, we can either define an enumeration tag or a genuine type using ```typedef```.
- Example in code for enum. tag : ```enum color {BLUE, RED, GREEN};```
- Example in code for enum. type : ```typedef enum  {BLUE, RED, GREEN} color;```