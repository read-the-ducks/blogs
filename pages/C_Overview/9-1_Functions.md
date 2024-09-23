---
title: "Functions in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_9-1_Functions
summary:
---

We've previously seen that functions are series of statements that have been grouped together and given a name. They allow us to avoid duplicate code, and can be used as building blocks to many complex programs.

### Function Definitions
- A function in C has the following general form :

```
return-type function-name (parameters)
{
    declarations
    statements
    return statement + arguments
}
```
- Functions can have a return-type ```void``` indicating that they do not return any value.
- In the standard C89, if a function has no return type specified (not even ```void```), it automatically expects to return ```int``` values.

### Function Calls
- Function calls consist of the function name, followed by parentheses. Any arguments we'd like to pass to the function must be in between parentheses. Also, if the function returns a value, it can be called in a statement where the retuned value is assigned to a variable using the assignment operator.
- Function cannot return arrays, however they can return pointers to arrays.
- Interestingly, every function has access to a ```__func``` identifier, which holds the name of the function which is currently executing. It is very interesting for debug purposes.

### Function Declarations in C
- The location of a function declaration matters in C, as the compiler goes from top-to-bottom. If a function is called before being declared, the compiler will create an **implicit declaration** of the function.
- C allows us to provide **function declarations** without needing to provide the full declaration itself. The function declaration must be consistent with the full definition of the function to avoid unexpected behavior. Example of a function declaration : ```return-type function-name ( parameters ) ;```.
- C allows us to combine function declarations and variable declarations for multiple functions on the same line. Example in code : ```double avg(int a, int b), median(int a, int b);```

### Function Arguments
- By default in C, arguments are passed by value. We can use pointers to pass values by reference.
- Interestingly, the comma operator is viewed differently if we encase it in parentheses. See ```int f(a,b)``` versus ```int f((a,b))```. 

### Argument Conversions
- C allows function calls in which the types of the arguments do not match the types of the parameters. The behavior of the compiler depends on whether a function prototype was made available before the function call.
- If the compiler encounters a function prototype, the value of each argument is implicitely converted to the type of the corresponding parameter as if by assignment.
- If the compiler does not encounter a function prototype, the compiler performs the default argument promotions (i.e. ```float``` to ```double```, ```char``` and ```short``` to ```int```).

### Array Arguments
- Arrays can be passed as parameters in C, without us being able to specify the length. However, if knowing the length is required in the function, we must pass the length of the array as a second parameter. Perform operations using the ```sizeof()``` operator to be able to retrieve the array length will not be successful
- A reference to an Array is a pointer, therefore if we pass an Array to a function, the function will always modify the values in the array by reference.
- The keyword ```const``` can be added before array parameters to ensure that there are no attempts to modify the array contents in the function body.

### Variable-Length Array Parameters (Standard C99)
- The standard *C99* allows us to specify the required array size in function prototype. This allows us to make our function prototypes more expressive & easier to understand.
- If we declare a variable length array as a function parameter, we must explicitely state that it's length parameter beforehand. 
- Bad Example in code : ```int sum_array(int a[n], int n)```.
- Good Example in code : ```int sum_array(int n, int a[n])```.
- Asterisks can also be used as a 'hint' that the length of an array is related to previous elements in the function parameter list. Example in code : ```int sum_array(int n, int a[*])```.

### Using *static* in Array Parameter Declarations
- Using the keyword ```static``` in the declaration of array parameters indicated that the length of an array is going to be at least equal to a specified value. Example in code : ```int sum_array(int n, int a[static 3])```.
- Using the keyword ```static``` can help with optimization, although it can only be applied to the first dimension of arrays.

### Compound Literals (Standard C99)
- Compound literals allow us to pass an array as a function parameter without needing to declare an array name. Example in code : ```int sum_array(int n, (int []) {1,2,3,4})```.
- To avoid undefined behavior, there must be a cast before the array parameter (i.e. ```(int []```)).

### The return statement
- Non-void functions must use the ```return``` statement to specify the value they will return back where they were originally called.
- Void functions can have a simple ```return``` statement with no parameters, or no ```return``` statement at all.

### Program Termination
- The ```main``` function in a program usually returns an integer. It is bad practice to set the program's ```return``` type to void, as the value returned by ```main``` is sometimes tested by the operating system when the program ends.

### Using the *exit* function
- To provoke program termination anywhere in the code, we can call the ```exit()``` function. It takes an integer as a parameter which acts as a termination code.
- Macros ```EXIT_SUCCESS``` and ```EXIT_FAILURE``` are defined in the standard library ```<stdlib.h>```, and can be used as substitute to integer values for comprehensivity's sake.