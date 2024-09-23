---
title: "Declarations in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_18-1_Declarations
summary:
---

Declarations play a central role in C programming. This section explores sophisticated option that can be used in declarations for both variables and functions. The concepts of storage duration, scope and linkage are explored.
### Declaration Syntax
- Declarations in C have the following appearance : ```declaration-specifiers declarators ;```. We are already familiar with Declarators, which provide the names and additional information about properties, but still have yet to see the different declaration specifiers.
- Declaration specifiers include (1) Storage classes, which include ```auto, static, extern, register```, (2) Type qualifiers, which include ```const, volatile, restrict```, (3) Type specifiers, which include ```void, char, short, int, long, float, double, signed, unsigned``` and any other specifications of structures, unions, enumerations, ```typedef``` type names, (4) Function specifier, which only includes the element ```inline```.
### Storage Classes
- Each variable in C has three properties : **Storage duration**, **Scope**, and **Linkage**.
- Storage duration determines when memory is set aside for a variable and when it is released. The two main types are *automatic storage duration* which releases allocated memory when the surrounding block is executed and *static storage duration* which ensures that the variable is stored until the total completion of the program.
- Scope, which is the portion of the program text where the variable can be referenced. A variable can either have a *block scope*, meaning that it is visible till the end of the block is was declared in, or a *file scope*, meaning that it is visible from the point of declaration till the end of the enclosed file.
- Linkage of a variable determines how a variable can be shared among different parts of a program. A variable with external linkage may be shared by several files in the program, while a program with internal linkage is restricted to a single file, although it can still be shared by the functions in that file. A variable with no linkage belongs to a single function and cannot be shared at all.
- The ```auto``` storage class is legal only for variables that belong to a block. It is assigned by default to variables that belong in a block. It offers automatic storage duration, block scope, and no linkage.
- The ```static``` storage class can be used with any variables, regardless of where they are declared. When used outside a block, ```static``` specifies that the variable has internal linkage. When used inside a block, ```static``` specifies that a variable's storage duration is static rather than automatic. The ```static``` storage class is used for information hiding, returning pointer values, and passing values between recursive function calls.
- The ```extern``` storage class enables multiple source files to share the same variable. ```extern``` variables have static storage durations, and their scope differs if they are in a block (block scope) or outside a block (file scope). The linkage of ```extern``` variables depends on whether the variable was declared static outside of any function definition, giving it an internal linkage, or not, giving it external linkage.
- The ```register``` storage class requests the compiler to store the variable in a CPU register instead of keeping it on main memory. The ```register``` storage class is only legal for variables declared in a block, while preserving the same storage duration, scope and linkage as an ```auto``` variables. The only exception is that ```register``` variables do not have set addresses, making it illegal to use the ```&``` operator. The ```register``` storage class is best used for variables that are accessed frequently in our program. Using the ```register``` storage class isn't as popular nowadays, because compilers assign it automatically to variables that would benefit from it (e.g. loop variables).
- For Function Declarations and Definitions, the storage classes that can be used are ```extern, static```. The ```extern``` storage class specifies that the function has external linkage, allowing it to be called from other files. The ```static``` storage class indicates internal linkage, limiting use of the function's name to the file in which it's defined. By default, functions have external linkage, making it redundant to call ```extern``` on a function (just like using ```auto``` on a block variable). For function parameters, the only storage class which can be used is ```register```.

### Type Qualifiers
- There are three type qualifiers : ```const```, ```volatile``` and ```restrict```.
- ```const``` is used to declare objects that resemble variables but are 'read-only'. They are mainly used for documentation purposes, or to identify data to be stored in ROM (e.g. embedded-systems use case). Unlike values defined with the ```#define``` directive, ```const``` values can be viewed directly in the debugger and can be used with the ```&``` operator.
- ```volatile``` is used to specify volatile memory locations, meaning that the value stored at such location can change as the program is running. It can be caused by data directly coming from input devices for example.
- ```restrict``` is used to specify that an object assigned to a pointer can only be accessed by using the pointer it is associated with. It is used for optimization purposes and to avoid a value being reloaded if we already have a pointer to its address.

### Declarators
- Declarators can take the form ```*, [], ()```. ```*``` represents a pointer, ```[]``` represent an array, and ```()``` represents a function. All the declarator types can be combined together.

### Initializers
- We've already talked about initializing variables previously for different types (e.g. integers, characters, etc).
- When variables are not initialized, the initial value of the variable depends on the storage duration : Variables with automatic storage duration have no default initial value (e.g. initialized to garbage), while variables with static storage duration values have the value zero by default (e.g. integer are zero, floats are 0.0, pointers point to null by default).

### Inline Functions (standard C99)
- The standard *C99* contains the keyword ```inline```, it was already part of GCC previously so watch out for any confusion when working with both of them.
- Looking back into assembly code, having a function call adds additional overhead and might not allow for much optimization. By requesting to ```inline``` a function, we basically ask to have the code of the function be integrated into the callee, as to perform both optimization between those two entities also.
- ```inline``` functions are already implemented heavily automatically by most compilers.