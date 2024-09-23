---
title: "Writing Large Programs in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_15-1_Writing-Large-Programs
summary:
---

Most C programs are not small enough to put in a single file. Typical C programs usually consists of several source files and header files. Source files contain definitions of functions and external variables, while header files contain information to be shared among source files.

### C Source Files
- C Source Files have the *.c* extension by default. They contain part of the program, mainly definitions of functions and variables. One of the source files must contain the main function, which serves as the entry point for the program.
- Splitting a program into multiple source files usually offer these advantages : (1) Grouping related functions & variables helps simplify the program structure, (2) Each source file can be compiled separately, which saves time if a program is large and must be compiled several times during development, (3) Functions can be more easily reused in other programs when grouped in separate source files.

### C Header Files
- C Header Files have the *.h* extension by default.
- Separing our program into source files brings up the following issues : How are we supposed to call a function that's defined in another file ? How can a function access an external variable in another file ? How can two files share the same macro or type definition ?
- The ```#include``` directive can be used to share information (i.e. function prototypes, macro/type definitions, etc) among different source files. This directive tells the preprocessor to open a specified file and insert its contents into the current file. Thus if we want several source files to have access to the same information, we'll put that information in a file and the use the ```#include``` directive to bring the file's content into each of the source files.

### Using the *#Include Directive*

- The ```#include``` directive has three primary form, one for C's own libraries and nother for header files written by the programmer.
- The first form is used for header files that belong to C's own libraries (e.g. ```#include <filename>```). The compiler search for these files in the directory where system header files reside (e.g. ```/usr/include``` on UNIX systems).
- The second form is used for header files written by programmers (e.g. ```#include "filename"```). The compiler usually searches in the same directory as the source code files, unless specified. It is better to give a relative path rather than an absolute path when including header files, as to not hinder portability.
- A less used third form is used for preprocessing tokens. The preprocessor will scan the tokens and replace any macros it finds. After macro replacement, the resulting directive must match one of the other forms of include. This is especially useful if we'd rather let filenames be defined by macros, then hardcoded.
- Example of the third form in code :

```c
#if defined(IA32)
    #define CPU_FILE "ia32.h"
#elif defined(IA64)
    #define CPU_FILE "ia64.h"
#endif

#include CPU_FILE
```

- It's important to note that it is very bad practice to include *.c* files in other source files, as it will cause unexpected issues. Try to only work with header files.

### Sharing Macro/Type Definitions
- Macro/Type Definitions should be included in header files, as to be shared amongst multiple source files.

### Sharing Function Prototypes
- If a source file contains a call to a function in another file with no prototype to rely on, the compiler is forced to assume the return type of the function, which might break the program is these assumptions are incorrect.
- To share a function, we put its **definition** in a source file, and we then put its **declaration** in other files that need to call the function. A good solution would be to add a function prototype inside of a header file. 
- Always include the header file declaring a function in the source file that contain that function's definition. Failure to do so can cause hard-to-find bugs, since calls of f elsewhere in the program might not match that function's definition.

### Sharing Variable Declarations
- External Variables can be shared among files in almost the same fashion as functions.
- Usually, to declare a variable we've used the following : ```int i;``` which declares an integer variable *i* and defines it as well by causing the compiler to set aside space for *i*. To declare *i* without defining it, we can use the keyword ```extern``` at the beginning of its declaration : ```extern int it;```.
- ```extern``` informs the compiler that *i* is defined elsewhere in the program/in another source file, so there is no need to allocate space for it. To avoid inconsistencies, the declaration of shared variables must be put in header files and each header file that contains a variable declaration must be included in the source file that contains the variable definition.

### Nested Includes
- Header files can include many ```#include``` directives, which is particularly useful if we'd like to have the same ```#include``` directives over many source files.

### Protecting Header Files
- If a source file includes the same header file twice,due to header files including other header files, it might lead to compilation errors. It's good practice to protect header files against multiple inclusions by enclose the contents of the file in an ```#ifndef``` and ```endif``` pair.
- Example in code :

```c
// If the BOOLEAN_H macro is not defined, the preprocessor will allow the lines between #ifndef and #endif to stay.
// If it is defined, then the contents will not be included.
#ifndef BOOLEAN_H
#define BOOLEAN_H

#define TRUE 1
#define FALSE 0
typedef int Bool;

#endif
```

### #error Directives in Header Files
- To avoid using header files designed for a previous C standard, we can include the ```#error``` directive in header files.
- Example in code :
```c
//Existence of the _STDC_ macro is being tested. It only exists for a specific version of the C standard.
#ifndef __STDC__
#error This header requires a specific version of C
#endif
```

### Building a Multiple-File Program
- We already talked about the process of compiling and linking a single-file program. What about multi-file programs ?

- The same steps are required when building a multi-file program : (1) Preprocessing, (2) Compiling, and (3) Linking. The compiling and linking steps vary when building for a multi-file program.

- In the Compilation process, each source file in the program must be compiled separately. Header files do not need to be compiled separately, because they will be automatically compiled whenever a source file that includes them is compiled. For each source file, the compiler generates a file containing object code, which have the *.o* extension in UNIX and the *.obj* extension in Windows.

- In the Linking process, the object files created in the compilation process, as well as the code for library function, to produce an executable file. The linker is also responsible for resolving external references left by the compiler (External references occur when a function in one file calls a function defined in another file or accesses a variable defined in another file).

- Here's the GCC command used to build a 3-file program : ```gcc -o myProgram file1.c file2.c file3.c```.

### Using Makefiles
- The concept of a makefile originated with UNIX. It is a file containing the information necessary to build a program, like the list of files that are part of a program and all dependencies among the files.
- Here is an example of a makefile :

```makefile
justify: justify.o word.o line.o
    gcc -o justify justify.o word.o line.o

justify.o : justify.c word.h line.h
    gcc -c justify.c

word.o: word.c word.h
    gcc -c word.c

line.o: line.c line.h
    gcc -c line.c
```

- In the previous example, there are four group of lines, with each specifying a certain **rule**. The first line in each rule specifies a **target** file, followed by which file it depends. The second line specifies the command to be executed if the file needs to be rebuilt because to a change to one of its dependent files.

### Errors during Linking
- Some errors that can't be detected during compilation will be detected during the linking process. More particularly, this happens if the definition of a function or variable is missing from a program. The linker will be unable to resolve external references to it, causing an error. These errors are mostly caused by misspellings, missing giles, or missing libraries.

### Rebuilding a Program
- During the development of a program, only the files that received modifications is usually recompilled. If changes affect a single source file, then it is recompilled on its own. If changes effect a header file, then all associated source files as well as the header file itself is recompilled.

### Defining Macros outside of a Program
- GCC allows us to specify the value of a macro when initializing compilation from the terminal with the *-D* flag. Any set value for the macro in our code will be overwritten.
- Example where we set the *DEBUG* variable to 1 ```gcc -DDEBUG=1 foo.c```