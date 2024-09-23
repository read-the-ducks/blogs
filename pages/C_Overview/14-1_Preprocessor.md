---
title: "Preprocessor in C Compilers"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_14-1_Preprocessor
summary:
---

We have already seen a set of preprocessor directives in previous chapters. Some of them include the ```#define``` and ```#include``` directives. The preprocessor is a piece of software that edits C programs prior to compilation. C, along with C++, both rely heavily on the preprocessor. Use of preprocessor directives should be moderated as it could both prove very useful in some situations, and cause hard-to-find issues if misused.

### How does the preprocessor operate ?
- The behavior of the preprocessor is controlled by **preprocessing directives**, which are commands beginning with a *#* character.
- The preprocessor receives a C program with directives as an input, and executes these directives before removing any mention of them (i.e. lines are not 'removed' but rather left empty). The output of the preprocessor is another C program containing no directives, which is given directly as an input to the compiler. The compiler will check the modified C program for errors and translate it to object code/machine instructions. The preprocessor used to be a separate component, but nowadays it is part of the compiler.
- In GCC, we can check the output of the preprocessor by using the ```-E``` tag.
- The preprocessor replaces comments with a single space.
- The preprocessor is not 'smart'. It has no knowledge and might output an incorrect program which will not compile for a certain set of directives.

### Rules of Preprocessing Directives
- Preprocessing Directives must respect the following : (1) They must always begin with a *#* symbol, (2) White spaces and tabs are fine between tokens in a preprocessing directive, (3) Directives always end at the first new-line character, unless explicitly continued using the *\\* character, (4) Directives can appear anywhere in the program (although they are usually included in the beginning), (5) Comments can appear in the same lines as directives.

### Exploring the different Preprocessing Directives
- The ```#define``` directive defines a **macro**, or a name that represents something else such as a constant. The preprocessor responds to this directive by storing the name of the macro together with its definiton. Whenever the macro is used in the program, the preprocessor replaces all mentions of the macro with its defined value. The ```#undef``` directive does the opposite : it removes a macro definition. Macro definitions remain in effect till the end of the file, unless we use the ```#undef``` directive to undefine them.
- The ```#include``` directive tells the preprocessor to open and include the contents of a particular file during compilation.
- The ```#if, #ifdef, #ifndef, #elif, #else, #endif``` directives allow block of text to be either included or excluded from the program depending on conditions that can be tested by the preprocessor.
- The directive ```#error```
- The directive ```#line```
- The directive ```#pragma```

### Simple Macros
- We can define **simple macros** as follow ```#define identifier replacement-list```. A macro's 'replacement-list' can include identifiers, keywords, numeric constants, character constants, string literals, operators, and punctuation. Be sure to not add extra characters, like semi-colons, in your macro definition, as the preprocessor will take them into consideration. 
- Using simple macros makes the program easier to read, modify, and helps avoid inconsistencies and typographical errors. They can also be used for specific applications like (1) making minor changes to the C syntax, (2) renaming types, (3) and controlling conditional compilation. 


- It is legal for a macro's replacement-list to be empty.

- Examples in code for some of the cases we've mentioned :

```c
#define BEGIN {
#define END }
#define BOOL int
#define debug    
```


- A macro's replacement-list can contain invocations to other macros. Example in code : 

```c
#define PI 3.14 
#define TWOPI (2*PI)
```



### Parametrized Macros
- We can define **parametrized macros** as follow ```#define identifier( <macro parameters> x1, x2 ...) replacement-list```. There must be no spaces between the identifier and the macro parameters. 
- Example of a parametrized macro in code :

```c
#define MAX(x,y) ((x)>(y)? (x):(y))
#define IS_EVEN(x) ((n)%2==0)

int main()
{
    int i, k;
    i = MAX(j+k, m-n);
    k = IS_EVEN(i);
}
```

- Parametrized macros can also have empty parameter lists : ```#define getchar() getc(stdin)```.
- Using parametrized macros can lead to better program performance, especially if we substitue a macro to a regular function call with overhead. In the standard *C99*, it is however a better option to use inline functions.
- Parametrized macros do not require specific function types for their parameters, this allows for flexibility, but might cause issues if the parameters passed have a type that does not operate well with the macro's operations. Also, if a function is called using a parametrized macro, the arguments passed will not be typed checked, which might lead to issues during compilation or undefined behavior.
- Unlike pointers to functions, it is not possible to have 'pointer to macros'.
- Using increment/decrement operators inside of macros might prove risky, especially if the macro has more than two 'checks' on a value (e.g. if/else statement in the macro).
- We can use macros to write patterns of code we are repeating a lot, like ```printf("%d\n", i);```, which can be defined as a macro as ```#define PRINT(x) printf("%d\n", i)```.
- In the standard *C99*, it is possible to leave some parameters of the macro empty, assuming it will not affect the operation of the function.

- In the standard *C99*, it is possible to have a variable number of macro parameters. To do so, we must use the ```...``` token in the macro parameter list, and the special identifier ```__VA_ARGS__``` to refer to these variable parameters in the replacement-list.

### The # and ## Operators
- Operators ```#, ##``` are only recognized by the preprocessor. 
- The ```#``` operator converts a macro argument to a string literal, which can be later used for debugging purposes. Example in code : ```#define PRINT(x) printf(#n " = %d\n", i)```. A line containing only the ```#``` operator counts as a **null directive** with no effect.
- The ```##``` operator provides a way to concatenate arguments during macro expansion. Example in code : ```#define GENERIC_MAX(type) \ type type##max(type x, type y){}```.

### Predefined Macros in C
- C offers several predefined macros, which each represent either an integer or string. They include (1) ```_LINE_```, which provides information on the line number of the file being compiled, (2) ```_FILE_```, which provides information on the name of the file being compiled (3) ```_DATE_```, which provides information on the date of compilation (4)  ```_TIME_```, which provides information on (5)  and ```_STDC_```, which provides information on.
- The standard *C99* offers additional macros, like (1) ```__STDC__HOSTED__``` (2) ```__STDC__VERSION__``` which displays of the C standard supported, (3) ```__STDC__IEC_559__``` which displays if IEC 60559 floating-point arithmetic is supported (4) ```__STDC__IEC__559_COMPLEX__``` which displays if IEC 60559 complex arithmetic is supported.


### Conditional Compilation
- The C preprocessor recognizes directives that support **conditional compilation**, which helps us include/exclude part of the program depending on the outcome of a test performed by the preprocessor. We can use the ```#if, #elif, #endif``` directives.
- Example in code :

```c
#define DEBUG 1
...
#if DEBUG
// Do something related to debugging
#endif
``` 

- We can use the ```defined``` operator to check if a macro is defined. It is equivalent to using the ```#ifdef``` macro. The ```#ifndef``` is similar, but it asserts if a macro is NOT defined.
- Example in code :

```c
#define DEBUG 1

#ifdef DEBUG
// do something related to debugging
#endif

#if defined(DEBUG)
// Same as above block
#endif
```

- We can use the directives ```#elif, #else``` to have multiple branches in conditional statements. These are especially useful to make our program portable, or compilable with compilers using different C versions. We can also disable a chunk of code that contains comments by using conditional directives, although you must watch out for the fact that comments are processed before preprocessor directives themselves (i.e. unterminated comments in a 'disabled' chunk of code may cause an error message).
- There are other interesting directives like ```#error``` which has the format ```#error <message>```, and which is used to terminate the program with an error message when necessary.

- Example in code :

```c
#if defined(WINDOWS)
// Case 1 : Windows
#elif defined(MAC_OS)
// Case 2 : MAC_OS
#elif defined(LINUX)
// Case 3 : LINUX
#else
#error No operating system specified
#endif

#if defined(__STDC__)
// Do something
#else
// Do something else
#endif

#if 0
// Code with comments
// Always ignored
#endif
```

### Miscellaneous Directives
- We've already mentioned the ```#error``` directive in the previous part, there is also the ```#line``` and the ```#pragma``` directives which are interesting, albeit rarely used.
- The ```#line``` directive is used to alter the way program lines are numbered. It takes the form ```#line <n>``` where *n* is the value we want to increment the overall line count by (i.e. lines now start being counted as n, n+1... rather than 0, 1...). It does not affect the program operation. A second form would be ```#line <n> <filename>```, which would also modify the current file's name, affecting the macros ```__FILE__``` and ```__LINE__```.
- The ```#pragma``` directive allows us to request special behavior from the compiler. It has the form ```#pragram <tokens>```. If the special behavior is unrecognized, the preprocessor will simply ignore it as it is not allowed to give an error message. There are no standard pragmas in *C89*, but some were introduced in *C99*, and are part of the C library.
- The standard *C99* introduces the ```_Pragma``` operator, which is similar to the ```#pragma``` directive, but also allows to work around some limitations of the preprocessor. By default, preprocessing directives cannot spawn other preprocessing directives. ```_Pragma``` is however an operator, and not a directive, allowing us to circumvent this restriction.
- Example in code :

```c
#define DO_PRAGMA(x) _Pragma(#x)
...
// This will spawn "#pragma GCC dependency "parse.y" after expansion
DO_PRAGMA(GCC dependency "parse.y")
```