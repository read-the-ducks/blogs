---
title: "Selection Statements in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_5-1_Selection-Statements
summary:
---

There are three types of statements in C : (1) Selection Statements, (2) Iteration Statements, and (3) Jump Statements. Here, we focus on Selection Statements, which include the ```if/else``` statement, and the ```switch``` statement.

### Logical Expressions in C
- To write logical expressions in C, we can use C's relational operators (```<, >, <=, >=```), C's equality operators (```==, !=```), or C's logical operators (```!, &&, ||```)

### If/Else statement in C
- Using brackets in ```if/else``` statements is a good idea, especially when we have cascaded ```if/else``` statements.
- Here is an example of a cascaded ```if/else``` statement in C :

```c
if(n < 20)
{
    // Do something
}
else if (n > 50)
{
    // Do something
}
else
{
    // Do something
}
```

- Simple ```if/else``` statements can also be expressed using conditional expressions : ``` i >= 0 ? i: 0```, which translates to *'If i is superior or equal to zero, return i, else return zero'*.

### Boolean values in C
- Boolean values have only been introduced in the *C99* standard as variables of type ```_Bool```. They can take a value of 0/1 to represent a false/true condition respectively.
- In previous iterations of C, integer values were mostly used as equivalent to booleans.

### Switch statements in C
- If we want to check a variable's value under multiple conditions, we can use the cascaded ```if/else``` statement as done previously. C offers an alternative with the ```switch``` statement.
- The ```break``` statement is used to 'exit' the switch statement once we reach a satisfying condition.
- The ```case``` statement is used to check whether the variable we have as parameter to the switch statement is equal to a certain value.
- The ```default``` statement is used as a check if the variable we have as a parameter to the switch statement does not satisfies any of defined cases.
- Here's an example of the ```switch``` statement in code :

```c
switch (grade)
{
    case 4 : printf("Excellent");
             break;
    case 3 : printf("Good");
             break;
    case 2 : printf("Average");
             break;
    case 1 : printf("Average");
             break;
    case 0 : printf("Average");
             break;
    default : printf("Illegal Grade");
             break;
}
```
