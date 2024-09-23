---
title: "Loops in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_6-1_Loops
summary:
---

### While Statement in C
- ```While``` loops in C have a **controlling expression** and a **loop body**.
- Be wary of infinite loops ! Your controlling expression must have a reachable target that can end the loop.
- Example of a ```While``` loop in code :

```c
while(i < n)
{
    i = i*2;
}
```

### Do/While Statement in C
- ```Do/While``` statements in C is similar to the ```While``` statement. The only difference is that the loop body is executed at least once, before the controlling expression is taken into consideration for further iterations.
- Example of a ```Do/While``` loop in code :

```c
i=10;
do 
{
    print("%d",i);
    i--;
}
while(i>0);
```

### For Statement in C
- ```For``` loops use a counting variable to iterate over a specified loop body.
- The counting variable can be initialized inside of the ```For``` statement, but it can as well be an existing variable initialized in a previous expression in the code. In the *C99* standard, we can declare & initialize a variable in the ```For``` statement directly.
- The comma operator can be used to initialize multiple variables in the ```For``` loop of the code.
- Example of a ```For``` loop in code :
```c
for (i=10; i> 0; i--)
{
    print("%d",i);
}
```

### Exiting from Loops in C
- To exit from a loop, we can use the ```break``` statement, which will exit the loop without continuing further iterations.
- We can also use the ```continue``` statement, which will stop the current loop iteration, and jump to the following one.
- We can jump out of a loop using the ```goto``` statement, which is very close to *jump* instructions in assembly. To use ```goto```, we must specify a label to go in our code.
- Example of ```goto``` :

```c
myLabel :
...
goto myLabel;
```

### Null statement in C
- ```Null``` statement is simply an empty statement (i.e. only has a semicolon). It is used mainly when we have empty loop bodies (i.e. our desired operation is already executed in the ```For``` statement).