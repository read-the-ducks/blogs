---
title: "C Fundamentals"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_2-1_C-Fundamentals
summary:
---

### Basic C Program

Here's an example Hello World program in C :

```c
// Include information about C's standard I/O library
#include <stdio.h> 

// 'main' function takes no parameters (hence 'void') and returns an integer value.
int main(void)
{
    // Prints "Hello World", the returns to the line
    printf("Hello World\n");

    // Returns the value 0 to the OS
    return 0;
}
```

### Introducing the C Compiler

We will use a compiler to convert this program to a form the machione can execute. This usually involves three steps for a C program :

1. *Preprocessing* : The C program is given to a **preprocessor**, which looks at directives (i.e. lines starting with a *'#'*) and modifies the code depending on these directives.
2. *Compilation* : The C program resulting from the preprocessing stage goes to a **compiler**, which 'compiles' the code, or translates it to machine instructions/object code.
3. *Linking* : The machine instructions/object code obtained at the compilation stage is combined by the **linker** with additional code needed to yield a complete executable program. This additional code includes any library functions (i.e. standard C library or external libraries) that are used by the program.

### C Language IDEs

Integrated Development Environments (IDEs) are software packages which allows us to edit, compile, link, execute, and even debug a program, without leaving our environment. There are many IDEs available online, each with a set of supported platforms.

### C Core Features

C programs require little "boilerplate" code, and mainly rely on three key language features : (1) Directives, (2) Statements, (3) and Functions. 

- Directives are commands intended for the preprocessor. They always begin with the character ```#```, and not include a semi-colon at the end. The ```#include``` tells the preprocessor to include information about a certain header/library/file in our program.

- Statements are commands executed when the program runs. They include function calls, assignments, and C statements like ```return``` or ```break```. Each statement in C must end with a semicolon, with the exception of the compound statement.

- Functions are a set of statements which have been grouped together, and been given a name. They are the building blocks from which a program is constructed. C functions fall into two categories : (1) Functions written by the programmer, (2) and Functions provided as part of the C implementation, or *library functions* supplied by the compiler. A C function can 'return' a value using the ```return``` statement, or can be 'void', and only execute a set of operations without returning anything. The only mandatory function in all C programs is ```main```, which is called automatically whenever a C program is executed.

### Comments in C

Comments in C programs can be added using ```///```, if they span a single line, or ```/* */```, if they span multiple lines. Be aware that using ```//``` to comment has only been made available starting with the *C99* standard.

### Variables in C

Data is stored in C using variables. Each variable has a type which specifies what kind of data it holds (i.e *int*, *float*). Each variable type requires a different quantity of memory when allocated, and also has a varying time performance associated with each operation. 

- Variables must be **declared** for the benefit of the compiler before we can assign a value to them in our program. To declare a variable, we must specify its associated *type* and a unique *identifier* or name, and then we can **assign** a value to them using the ```=``` operator. To assign a value to a variable, we can use constants, operators and existing variables. Multiple variables can be initialized to a constant in a single line (e.g. ```int x, y, z = 10```)

- Please note that identifiers are case-sensitive, and can contain letters, digits and underscores, and also *must* begin with a letter or underscore. 

- Example of integer constants : ``` 5, 10, 3``` ;  Example of float constants : ``` 242.53f , 152.53f```

- A variable which is not assigned a value is said to be **unintialized**, or holding a 'garbage' value. Depending on the storage duration of a variable (static vs automatic),it is either initialized to zero automatically, or initialized to garbage.

### Defining constants in a C program
- Giving a name to constants we are using in our C programs make it easier to understand their purpose in the code, especially for programmers not familiar with your code.

- We can name our constants using *macro definitions*, with the ```#define``` preprocessing directive. When the program is compiled, the preprocessor replaces each macro by the value it represents.

- Example of macro definitions : ```#define PI (3.14f)```, ```#define MYWEIGHT (230f/2f)```
- Example of macro usage : ```int circleRadius = 2 * PI * radius```

### Keywords in C
Here is a list of keywords which have a special significance in C, and which cannot be used to identify variables : *auto, break, case, char, const, continue, default, do, double, else, enum, extern, float, for, goto, if, **inline**, int, long, register, **restrict**, return, short, signed, sizeof, static, struct, switch, typedef, union, unsigned, void, volatile, while, **_Bool**, **_Complex**, **_Imaginary***. (Keywords in Bold are only available on *C99*).

### C-Program Layout
C programs are a series of **tokens**, or group of characters that can't be split up without changing their meaning. Identifiers and keywords are tokens, and so are operators, punctuation marks, semicolon, and string literals. Tokens are crucial for the compiler to be able to read and understand our code.

### What is GCC ?

- GCC is a popular C compiler available on many platforms. The GCC acronym originally stood for "*GNU C Compiler*", it now stands for "*GNU Compiler Collection*" because the current version of GCC compiles programs in a variety of languages like C++, Java, and Fortran. 
- In the above acronym, GNU stands for *"GNU's not UNIX!"*. GNU is a project of the Free Software Foundation set-up to protests against the restrictions of licensed UNIX software. Much of the traditional UNIX software has been rewritten from scratch and made available publicly. 
- GCC and GNU are crucial to Linux. Linux is only the kernel component of the OS (i.e. Part of the OS which handles I/O services and program scheduling), and GNU software is fully functional operating system.
- GCC can run under many operating systems and can generate code for many CPU types. It is also the primary compiler for UNIX-based OSes, like Linux.
- To compile C code using GCC, we can use the command ```gcc -o myFile myFile.c```, which will compile a file called *myFile.c* and give a resultant executable program named *myFile.out*.
- GCC offers various command-line options to check programs in detail for errors. These include ```-Wall```, which produces warning whenever it detects possible errors, ```-W``` issues more warning messages beyond those produced by ```-Wall```, ```-pedantic``` issues all warnings required by the C standard while flagging all non-standard C features, ```-ansi``` turns off features of GCC that aren't standard C and enables some additional features, ```-std=c89``` allows us to specify which version of C should we use to check the program (Here it is *C89*). ```-O``` allows us to specify the level of optimization of our code, with higher levels of ```-O``` meaning higher optimization.